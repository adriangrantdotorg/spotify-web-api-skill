# 🤖🔊 Spotify Web API Agentic Skill

![Spotify Web API Agentic Skill Banner](banner.png)

> An Agent Skill for the Spotify Web API that teaches AI agents best practices for building robust, rate-limit-aware applications.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Anthropic-purple)](https://claude.ai)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Google-blue)](https://github.com/google-gemini/gemini-cli)
[![Codex CLI](https://img.shields.io/badge/Codex%20CLI-OpenAI-green)](https://github.com/openai/codex)
[![Cursor](https://img.shields.io/badge/Cursor-AI%20IDE-orange)](https://cursor.sh)
[![OpenCode](https://img.shields.io/badge/OpenCode-CLI-gray)](https://github.com/opencode-ai/opencode)
[![Antigravity](https://img.shields.io/badge/Antigravity-DeepMind-red)](https://github.com/sickn33/antigravity-awesome-skills)
[![Agent Skills Standard](https://img.shields.io/badge/Agent%20Skills-Standard-blue.svg)](https://github.com/anthropics/skills)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

Transform your AI coding assistant into a Spotify integration expert with battle-tested patterns for handling rate limits, smart polling, and efficient data fetching.

---

## ✨ Features

This skill equips AI agents with specialized knowledge to:

- ⚡ **Handle Rate Limits Gracefully** - Implement proper 429 error handling with `Retry-After` header extraction
- 🔄 **Smart Polling Strategies** - Dynamic interval adjustment using the Page Visibility API
- 📊 **Optimize Data Fetching** - Maximize page sizes and minimize API calls
- 🔐 **Manage OAuth Authentication** - Best practices for SpotifyOAuth configuration
- 🎯 **Choose the Right API** - Clear guidance on Web API vs Web Playback SDK
- 🛡️ **Build Resilient Apps** - Server-side fail-fast patterns to prevent thread blocking

---

## 📋 Prerequisites

To use this skill with Spotify integrations, you'll need:

- **Spotify Developer Account** - [Register here](https://developer.spotify.com/)
- **Spotify App Credentials**:
  - `SPOTIPY_CLIENT_ID` - Your app's client ID
  - `SPOTIPY_CLIENT_SECRET` - Your app's client secret
  - `SPOTIPY_REDIRECT_URI` - OAuth callback URL

Set these as environment variables or configure them in your development environment.

---

## 🚀 Installation & Integration

This skill follows the [Agent Skills open standard](https://github.com/anthropics/skills) and is compatible with multiple AI coding platforms.

### Quick Reference Table

| **Platform** | **Type** | **Installation Path** | **Invocation** |
|-------------|----------|----------------------|----------------|
| **Claude Code** | CLI | `~/.claude/skills/spotify-web-api/` | `Use the Spotify Web API skill...` or `/spotify-web-api` |
| **Claude.ai** | Web | Upload via Settings → Skills | Automatically invoked when relevant |
| **Google Antigravity** | IDE | `.agent/skills/spotify-web-api/` | Automatically invoked when relevant |
| **OpenCode** | IDE | `~/.config/opencode/skills/spotify-web-api/` | `skill({ name: "spotify-web-api" })` |
| **Cursor IDE** | IDE | `.cursor/skills/spotify-web-api/` | Mentioned in chat with `@spotify-web-api` |
| **OpenAI Codex** | CLI | `~/.codex/skills/spotify-web-api/` | Automatically invoked when relevant |
| **Gemini CLI** | CLI | `~/.gemini/skills/spotify-web-api/` | Automatically invoked when relevant |

### Detailed Installation Instructions

#### **Option 1: Clone from GitHub** (Recommended)

```bash
# For Claude Code (personal skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git ~/.claude/skills/spotify-web-api

# For Google Antigravity (project skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git .agent/skills/spotify-web-api

# For OpenCode (global skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git ~/.config/opencode/skills/spotify-web-api

# For Cursor (project skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git .cursor/skills/spotify-web-api

# For OpenAI Codex (global skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git ~/.codex/skills/spotify-web-api

# For Gemini CLI (global skills)
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git ~/.gemini/skills/spotify-web-api
```

#### **Option 2: Manual Installation**

1. Download the [latest release](https://github.com/adriangrantdotorg/spotify-web-api-skill/releases)
2. Extract the `spotify-web-api` folder
3. Copy to the appropriate skills directory for your platform (see table above)
4. Ensure `skill/spotify-web-api/SKILL.md` exists
5. Restart your AI assistant or reload the workspace

#### **Option 3: Claude.ai Upload**

1. Navigate to **Settings** → **Capabilities** → **Skills**
2. Click **Upload skill**
3. Select the ZIP file containing the skill folder
4. Toggle the skill **ON**

---

## 💡 Usage Examples

Once installed, your AI agent will automatically apply these best practices when working with Spotify. Here are some natural language prompts to try:

### Creating a New Integration

```
"Create a Python Flask app that displays my currently playing track with proper rate limit handling"
```

The agent will:
- Configure `spotipy` with fail-fast retry settings
- Implement 429 error handling with `Retry-After` extraction
- Add user-friendly countdown UI for rate limit waits

### Building a Dashboard

```
"Build a dashboard that polls my playback state every 10 seconds"
```

The agent will:
- Implement the Page Visibility API pattern
- Adjust polling from 10s (active) to 60s (hidden tab)
- Use `limit=50` for any list fetches

### Optimizing Existing Code

```
"Review this Spotify integration code and optimize it for rate limits"
```

The agent will:
- Audit retry configurations
- Check for proper error handling
- Suggest smart polling improvements
- Verify maximum page sizes are used

---

## 🤝 Contributing

We'd love contributions from the community, thanks! Whether you're fixing bugs, adding examples, or improving documentation, your help makes this skill better for everyone 🙌🏾

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines on:

- Setting up your development environment
- Coding standards and best practices
- Submitting pull requests
- Adding new examples
- Reporting issues

**Quick Start for Contributors:**

```bash
# Fork and clone the repository
git clone https://github.com/adriangrantdotorg/spotify-web-api-skill.git
cd spotify-web-api-skill

# Create a feature branch
git checkout -b feature/your-feature-name

# Make your changes and test them
# (Install in your local skills directory and test with your AI agent)

# Commit and push
git commit -m "Add: description of your changes"
git push origin feature/your-feature-name

# Open a Pull Request on GitHub
```

---

## 📚 Additional Resources

- **[Spotify Web API Documentation](https://developer.spotify.com/documentation/web-api)** - Official API reference
- **[Spotipy Library](https://spotipy.readthedocs.io/)** - Python client documentation
- **[Agent Skills Specification](https://github.com/anthropics/skills)** - Open standard documentation
- **[Rate Limiting Guide](https://developer.spotify.com/documentation/web-api/concepts/rate-limits)** - Spotify's official rate limit documentation

---

## 🐛 Issues & Support

Encountered a problem or have a suggestion?

- **Bug Reports**: [Open an issue](https://github.com/adriangrantdotorg/spotify-web-api-skill/issues/new?template=bug_report.md)
- **Feature Requests**: [Request a feature](https://github.com/adriangrantdotorg/spotify-web-api-skill/issues/new?template=feature_request.md)
- **Issues**: [View Issues](https://github.com/adriangrantdotorg/spotify-web-api-skill/issues)

---

## ⭐ Show Your Support

If this skill helped you build better Spotify integrations, please give it a star - thanks! ⭐

---




<div align="center">
  <sub>Built with ❤️ for Music Lovers & the Open Source Community ✌🏾</sub>
</div>
