---
name: github
description: "Git and GitHub integration for code management, repository operations, and collaboration. Use when users need to: (1) Push code to GitHub repositories, (2) Clone or interact with repositories, (3) Manage branches, commits, or pull requests, (4) View repository contents or history, (5) Configure git settings, or (6) Work with GitHub-hosted code. Always provide GitHub links when code is pushed."
---

# GitHub Integration

This skill enables comprehensive Git and GitHub operations, from basic version control to advanced repository management.

## Core Workflow

### 1. Repository Setup

**For existing repositories:**
```bash
git clone <repository-url>
cd <repository-name>
```

**For new repositories:**
```bash
git init
git remote add origin <repository-url>
```

### 2. Basic Git Operations

**Check status:**
```bash
git status
```

**Stage changes:**
```bash
git add .                    # Stage all changes
git add <specific-file>      # Stage specific file
```

**Commit changes:**
```bash
git commit -m "Descriptive commit message"
```

**Push to GitHub:**
```bash
git push origin <branch-name>
```

### 3. Branch Management

**Create and switch to new branch:**
```bash
git checkout -b <branch-name>
```

**Switch between branches:**
```bash
git checkout <branch-name>
```

**List branches:**
```bash
git branch
```

## Critical Rule: Always Provide GitHub Links

**IMPORTANT:** Whenever code is pushed to GitHub, ALWAYS include a direct link to the code in your response.

### Link Formats

**Repository:** `https://github.com/<username>/<repo>`

**Specific file:** `https://github.com/<username>/<repo>/blob/<branch>/<path-to-file>`

**Commit:** `https://github.com/<username>/<repo>/commit/<commit-hash>`

**Branch:** `https://github.com/<username>/<repo>/tree/<branch-name>`

**Pull request:** `https://github.com/<username>/<repo>/pull/<pr-number>`

### Example Response After Push

```
Successfully pushed your code to GitHub!

View your code here: <insert the Github commit URL here>
```

### Accuracy Check

Always verify the commit URL is accurate by confirming all code was successfully pushed before providing the link. Use `git log` to get the correct commit hash and construct the proper commit URL.

## Common Workflows

### Creating a New Project and Pushing to GitHub

1. Initialize repository locally or on GitHub
2. Create project files
3. Configure git (if first time):
   ```bash
   git config user.name "Your Name"
   git config user.email "your.email@example.com"
   ```
4. Add, commit, and push:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push -u origin main
   ```
5. **Provide commit URL:** Get commit hash with `git log -1 --format=%H` and share: `https://github.com/<username>/<repo>/commit/<commit-hash>`

### Updating Existing Code

1. Make changes to files
2. Review changes: `git diff`
3. Stage and commit:
   ```bash
   git add .
   git commit -m "Description of changes"
   git push
   ```
4. **Provide commit URL:** Get commit hash with `git log -1 --format=%H` and share: `https://github.com/<username>/<repo>/commit/<commit-hash>`

### Working with Branches

1. Create feature branch: `git checkout -b feature-name`
2. Make changes and commit
3. Push branch: `git push -u origin feature-name`
4. **Provide link:** Share link to the branch

## Authentication

### SSH (Recommended)

Check for existing SSH key:
```bash
ls -la ~/.ssh
```

Generate new SSH key:
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

Add to ssh-agent and copy to GitHub settings.

### Personal Access Token

For HTTPS authentication, use a personal access token instead of password.

## Troubleshooting

### Push Rejected
```bash
git pull origin <branch-name> --rebase
git push origin <branch-name>
```

### Merge Conflicts
```bash
git status                    # Identify conflicted files
# Manually resolve conflicts in files
git add <resolved-files>
git commit -m "Resolve merge conflicts"
git push
```

### Undo Last Commit (Not Pushed)
```bash
git reset --soft HEAD~1       # Keep changes staged
git reset HEAD~1              # Keep changes unstaged
git reset --hard HEAD~1       # Discard changes
```

## Advanced Operations

### View Repository Information
```bash
git remote -v                 # Show remote URLs
git log --oneline             # View commit history
git branch -a                 # Show all branches
```

### Stashing Changes
```bash
git stash                     # Save changes temporarily
git stash pop                 # Restore stashed changes
git stash list                # View all stashes
```

### Fetching Updates
```bash
git fetch origin              # Download latest changes
git pull origin <branch>      # Fetch and merge
```

## Link Formatting Best Practices

- Always use commit URLs when code has been pushed: `https://github.com/<username>/<repo>/commit/<commit-hash>`
- Use the full GitHub URL, not shortened versions
- Link to the specific branch where code was pushed
- For multi-file pushes, link to the commit URL to show all changes
- Include the commit hash in links when referencing specific versions
- For pull requests, link to the PR page after creation

## GitHub-Specific Features

### Creating Pull Requests
After pushing a branch, GitHub often shows a link to create a PR. Share this with the user.

### GitHub Actions
Reference workflows at: `https://github.com/<username>/<repo>/actions`

### Releases
View releases at: `https://github.com/<username>/<repo>/releases`
# Git Commands Quick Reference

This reference provides comprehensive Git commands organized by category for quick lookup.

## Configuration

```bash
# Set user information
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# View configuration
git config --list
git config user.name

# Set default branch name
git config --global init.defaultBranch main

# Set default editor
git config --global core.editor "vim"
```

## Repository Initialization

```bash
# Initialize new repository
git init

# Clone existing repository
git clone <url>
git clone <url> <directory-name>

# Add remote
git remote add origin <url>

# View remotes
git remote -v

# Change remote URL
git remote set-url origin <new-url>
```

## Staging and Committing

```bash
# Check status
git status
git status -s    # Short format

# Stage files
git add <file>
git add .
git add -A       # All changes
git add -p       # Interactive staging

# Unstage files
git restore --staged <file>
git reset HEAD <file>

# Commit changes
git commit -m "Message"
git commit -am "Message"    # Stage and commit tracked files
git commit --amend          # Amend last commit
```

## Branching

```bash
# List branches
git branch
git branch -a    # All branches (including remote)
git branch -r    # Remote branches

# Create branch
git branch <branch-name>

# Switch branch
git checkout <branch-name>
git switch <branch-name>

# Create and switch
git checkout -b <branch-name>
git switch -c <branch-name>

# Delete branch
git branch -d <branch-name>     # Safe delete
git branch -D <branch-name>     # Force delete

# Rename branch
git branch -m <new-name>        # Rename current branch
git branch -m <old> <new>       # Rename specific branch
```

## Merging and Rebasing

```bash
# Merge branch into current
git merge <branch-name>

# Abort merge
git merge --abort

# Rebase current branch onto another
git rebase <branch-name>

# Interactive rebase
git rebase -i HEAD~<number>

# Abort rebase
git rebase --abort

# Continue after resolving conflicts
git rebase --continue
```

## Pushing and Pulling

```bash
# Push to remote
git push
git push origin <branch-name>
git push -u origin <branch-name>    # Set upstream
git push --force                     # Force push (use carefully)
git push --force-with-lease          # Safer force push

# Pull from remote
git pull
git pull origin <branch-name>
git pull --rebase                    # Rebase instead of merge

# Fetch from remote
git fetch
git fetch origin
git fetch --all
```

## Viewing History

```bash
# View commit history
git log
git log --oneline
git log --graph
git log --graph --oneline --all
git log -<number>               # Last N commits
git log --author="Name"

# View changes
git diff                        # Working directory vs staging
git diff --staged               # Staging vs last commit
git diff <commit1> <commit2>    # Between commits
git diff <branch1> <branch2>    # Between branches

# Show commit details
git show <commit-hash>
git show HEAD                   # Latest commit
git show HEAD~1                 # Previous commit
```

## Undoing Changes

```bash
# Discard working directory changes
git restore <file>
git checkout -- <file>

# Unstage file
git restore --staged <file>
git reset HEAD <file>

# Undo commits (keep changes)
git reset --soft HEAD~1

# Undo commits (unstage changes)
git reset HEAD~1
git reset --mixed HEAD~1

# Undo commits (discard changes)
git reset --hard HEAD~1

# Revert commit (create new commit)
git revert <commit-hash>
```

## Stashing

```bash
# Stash changes
git stash
git stash save "Message"

# List stashes
git stash list

# Apply stash
git stash apply             # Latest stash
git stash apply stash@{n}   # Specific stash

# Apply and remove stash
git stash pop

# Remove stash
git stash drop stash@{n}

# Clear all stashes
git stash clear

# View stash contents
git stash show
git stash show -p
```

## Tagging

```bash
# Create tag
git tag <tag-name>
git tag -a <tag-name> -m "Message"    # Annotated tag

# List tags
git tag
git tag -l "v1.*"                      # Filter tags

# Push tags
git push origin <tag-name>
git push origin --tags                 # All tags

# Delete tag
git tag -d <tag-name>                  # Local
git push origin :refs/tags/<tag-name>  # Remote
git push origin --delete <tag-name>    # Remote (alternative)
```

## Collaboration

```bash
# View remote branches
git branch -r

# Track remote branch
git checkout --track origin/<branch-name>

# Update local list of remote branches
git fetch --prune

# View who changed what
git blame <file>

# Find commits that introduced a bug
git bisect start
git bisect bad          # Current version is bad
git bisect good <commit> # Known good commit
```

## Cleaning

```bash
# Remove untracked files (dry run)
git clean -n

# Remove untracked files
git clean -f

# Remove untracked files and directories
git clean -fd

# Remove ignored files too
git clean -fdx
```

## GitHub-Specific Operations

```bash
# Clone with SSH
git clone git@github.com:username/repo.git

# Clone with HTTPS
git clone https://github.com/username/repo.git

# Fork workflow
git remote add upstream <original-repo-url>
git fetch upstream
git merge upstream/main
```

## Advanced Operations

```bash
# Cherry-pick commit
git cherry-pick <commit-hash>

# Find commit that introduced string
git log -S "string"

# Search commit messages
git log --grep="pattern"

# View file at specific commit
git show <commit>:<file>

# List files in commit
git show --name-only <commit>

# Compare file across branches
git diff <branch1> <branch2> -- <file>
```

## Shortcuts and Aliases

Common aliases to add to your `.gitconfig`:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.lg 'log --graph --oneline --all'
```
# GitHub Best Practices and URL Reference

This reference provides GitHub-specific best practices, URL patterns, and workflow recommendations.

## GitHub URL Patterns

### Repository URLs

- **Main repository:** `https://github.com/<username>/<repo>`
- **Clone SSH:** `git@github.com:<username>/<repo>.git`
- **Clone HTTPS:** `https://github.com/<username>/<repo>.git`

### File and Directory URLs

- **File on branch:** `https://github.com/<username>/<repo>/blob/<branch>/<path>`
- **Directory on branch:** `https://github.com/<username>/<repo>/tree/<branch>/<path>`
- **File at commit:** `https://github.com/<username>/<repo>/blob/<commit-hash>/<path>`
- **Raw file:** `https://raw.githubusercontent.com/<username>/<repo>/<branch>/<path>`

### Commit and History URLs

- **Specific commit:** `https://github.com/<username>/<repo>/commit/<commit-hash>`
- **Commit range:** `https://github.com/<username>/<repo>/compare/<commit1>...<commit2>`
- **Commits page:** `https://github.com/<username>/<repo>/commits/<branch>`

### Branch and Tag URLs

- **Branch view:** `https://github.com/<username>/<repo>/tree/<branch-name>`
- **All branches:** `https://github.com/<username>/<repo>/branches`
- **Tags:** `https://github.com/<username>/<repo>/tags`
- **Releases:** `https://github.com/<username>/<repo>/releases`
- **Specific release:** `https://github.com/<username>/<repo>/releases/tag/<tag-name>`

### Pull Request URLs

- **All PRs:** `https://github.com/<username>/<repo>/pulls`
- **Specific PR:** `https://github.com/<username>/<repo>/pull/<number>`
- **PR files:** `https://github.com/<username>/<repo>/pull/<number>/files`
- **PR commits:** `https://github.com/<username>/<repo>/pull/<number>/commits`

### Issue URLs

- **All issues:** `https://github.com/<username>/<repo>/issues`
- **Specific issue:** `https://github.com/<username>/<repo>/issues/<number>`

### Other URLs

- **Actions:** `https://github.com/<username>/<repo>/actions`
- **Specific workflow:** `https://github.com/<username>/<repo>/actions/workflows/<workflow-file>`
- **Projects:** `https://github.com/<username>/<repo>/projects`
- **Wiki:** `https://github.com/<username>/<repo>/wiki`
- **Settings:** `https://github.com/<username>/<repo>/settings`

## Commit Message Best Practices

### Format

```
<type>: <subject>

<body>

<footer>
```

### Types

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting, etc.)
- `refactor:` Code refactoring
- `test:` Adding or updating tests
- `chore:` Maintenance tasks
- `perf:` Performance improvements

### Examples

```bash
git commit -m "feat: add user authentication"

git commit -m "fix: resolve null pointer exception in login handler"

git commit -m "docs: update API documentation for v2.0"
```

### Good Commit Messages

- Use imperative mood ("add" not "added" or "adds")
- Keep subject line under 50 characters
- Capitalize subject line
- Don't end subject with period
- Separate subject from body with blank line
- Wrap body at 72 characters
- Use body to explain what and why, not how

## Branch Naming Conventions

### Common Patterns

- `feature/<feature-name>` - New features
- `bugfix/<bug-name>` - Bug fixes
- `hotfix/<issue>` - Urgent fixes
- `release/<version>` - Release branches
- `docs/<description>` - Documentation updates

### Examples

```bash
git checkout -b feature/user-authentication
git checkout -b bugfix/login-error
git checkout -b hotfix/security-patch
git checkout -b docs/api-guide
```

## Pull Request Best Practices

### PR Title Format

Similar to commit messages:
- `feat: Add user profile page`
- `fix: Resolve database connection issue`
- `docs: Update README with installation steps`

### PR Description Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- How was this tested?
- Test cases added/updated?

## Checklist
- [ ] Code follows project style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Tests added/updated
- [ ] All tests passing
```

## GitHub Workflows

### Standard Feature Development

```bash
# 1. Create feature branch
git checkout -b feature/new-feature

# 2. Make changes and commit
git add .
git commit -m "feat: implement new feature"

# 3. Push to GitHub
git push -u origin feature/new-feature

# 4. Create pull request on GitHub
# Provide link: https://github.com/username/repo/pull/NEW_PR_NUMBER

# 5. After review and approval, merge PR
# 6. Delete feature branch
git branch -d feature/new-feature
git push origin --delete feature/new-feature
```

### Hotfix Workflow

```bash
# 1. Create hotfix from main
git checkout main
git checkout -b hotfix/critical-bug

# 2. Fix and commit
git add .
git commit -m "hotfix: fix critical security issue"

# 3. Push and create PR
git push -u origin hotfix/critical-bug

# 4. After merge, update local main
git checkout main
git pull origin main
```

### Syncing Fork

```bash
# 1. Add upstream remote (once)
git remote add upstream https://github.com/original/repo.git

# 2. Fetch upstream changes
git fetch upstream

# 3. Merge upstream into local main
git checkout main
git merge upstream/main

# 4. Push to your fork
git push origin main
```

## Security Best Practices

### Sensitive Information

- Never commit passwords, API keys, or tokens
- Use environment variables or config files (gitignored)
- Use `.gitignore` to exclude sensitive files
- Check `.env` files are in `.gitignore`

### SSH Key Management

```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Start ssh-agent
eval "$(ssh-agent -s)"

# Add key to agent
ssh-add ~/.ssh/id_ed25519

# Copy public key to GitHub settings
cat ~/.ssh/id_ed25519.pub
```

## Common .gitignore Patterns

```gitignore
# Dependencies
node_modules/
venv/
env/
__pycache__/

# Environment variables
.env
.env.local
*.env

# IDE
.vscode/
.idea/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Build outputs
dist/
build/
*.pyc
*.log

# Secrets
secrets.json
config/secrets.yaml
```

## GitHub Features to Reference

### Actions
- Link to workflows: `https://github.com/username/repo/actions`
- Mention CI/CD status when relevant

### Releases
- Link to releases when mentioning versions
- Format: `https://github.com/username/repo/releases`

### Issues
- Reference issues in commits: `fixes #123` or `closes #456`
- Link directly when discussing bugs

### Projects
- Link to project boards when discussing tasks
- Format: `https://github.com/username/repo/projects`

## Link Formatting in Responses

When providing GitHub links after operations:

### After Pushing Code
```
Successfully pushed to GitHub!

📦 Repository: https://github.com/username/repo
📄 File: https://github.com/username/repo/blob/main/src/app.py
```

### After Creating Branch
```
New branch created and pushed!

🌿 Branch: https://github.com/username/repo/tree/feature/new-feature
```

### After Committing
```
Changes committed successfully!

📝 Latest commit: https://github.com/username/repo/commit/abc123def456
```

### For Pull Requests
```
Pull request ready for review!

🔀 PR: https://github.com/username/repo/pull/42
```
