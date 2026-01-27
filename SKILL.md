---
name: spotify-web-api
description: "Best practices and workflows for the Spotify Web API. Use when building apps that interact with Spotify to: (1) Handle rate limits and 429 errors, (2) Implement efficient polling strategies, (3) Optimize data fetching, or (4) Manage authentication. Includes specific patterns for 'Smart Polling' and 'Retry-After' handling."
---

# Spotify Web API Skill

This skill encodes best practices for building robust, rate-limit-aware applications using the Spotify Web API.

## 1. Rate Limiting Strategy (Critical)

Spotify uses a dynamic, rolling 30-second window for rate limiting. There is no fixed "requests per hour" limit.

### Handling 429 Response
You **must** handle HTTP 429 (Too Many Requests) errors gracefully.

**Server-Side (Python/Spotipy):**
1.  **Do not block:** Configure the client to fail fast rather than retrying indefinitely and blocking your server threads.
2.  **Extract Header:** Capture the `Retry-After` header from the response. This integer tells you exactly how many seconds to wait.
3.  **Pass to Client:** Return this value to your frontend so the UI can inform the user.

```python
# app.py example
sp = spotipy.Spotify(auth_manager=auth, requests_timeout=10, status_retries=0, retries=0)

try:
    sp.current_user_playing_track()
except spotipy.exceptions.SpotifyException as e:
    if e.http_status == 429:
        retry_after = int(e.headers.get('Retry-After', 5)) # Default to 5s if missing
        return jsonify({"error": "Rate limit", "retry_after": retry_after}), 429
```

**Client-Side (JavaScript):**
1.  **Backoff:** If you receive a 429, respect the `retry_after` value.
2.  **User Feedback:** Display a countdown (e.g., "Retrying in X seconds...") so the user knows the app isn't broken.

## 2. Polling Best Practices

### Safe Intervals
*   **Active Tab:** Poll no faster than every **5-10 seconds**.
*   **Background:** Significantly reduce polling frequency when the user is not actively viewing the page.

### 'Smart Polling' Pattern (Page Visibility API)
Use the Page Visibility API to dynamically adjust polling rates. This saves your "request budget" for when the user is actually looking at the dashboard.

```javascript
// script.js example
let pollInterval = 10000; // 10s default

document.addEventListener('visibilitychange', () => {
    if (document.hidden) {
        console.log("Tab hidden, slowing down to 60s");
        pollInterval = 60000;
    } else {
        console.log("Tab visible, restoring to 10s");
        pollInterval = 10000;
    }
});

function poll() {
    // ... fetch logic ...
    setTimeout(poll, pollInterval);
}
```

## 3. Data Fetching Optimization

### Maximize Page Size
Always request the maximum number of items allowed per call (usually `limit=50` or `limit=100`) to minimize the total number of HTTP requests.

**Before (Inefficient):**
```python
# Default limit is often 20
results = sp.playlist_items(playlist_id) 
```

**After (Optimized):**
```python
# Fetch 100 items at once
results = sp.playlist_items(playlist_id, limit=100) 
```

## 4. Authentication

Use `spotipy.oauth2.SpotifyOAuth` for robust OAuth 2.0 flow handling.

*   **Scopes:** Be specific. Only request scopes you actually need.
*   **Token Caching:** Spotipy handles caching automatically (`.cache` file), but ensure you handle token validation and refreshing logic if building a long-running server.

```python
def get_auth_manager():
    return SpotifyOAuth(
        client_id=os.getenv("SPOTIPY_CLIENT_ID"),
        client_secret=os.getenv("SPOTIPY_CLIENT_SECRET"),
        redirect_uri=os.getenv("SPOTIPY_REDIRECT_URI"),
        scope="user-read-playback-state user-library-read",
        open_browser=False # Important for server environments
    )
```

## 5. Web API vs. Web Playback SDK

*   **Web API:** Use for **Dashboards** and **Controllers**. You want to see what is playing on *any* device or control playback remotely.
*   **Web Playback SDK:** Use for **Music Players**. You want the browser tab itself to emit sound and act as a Spotify Connect device. Do not use this just for metadata.
