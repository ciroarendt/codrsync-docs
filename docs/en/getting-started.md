# Getting Started

## Prerequisites

- Python 3.10 or higher
- One of: pip, pipx, Homebrew, or npm
- API key for AI features (Anthropic, OpenAI, or codrsync cloud)

## Installation

### Option 1: Install Script (Recommended)

```bash
curl -fsSL https://codrsync.dev/install.sh | bash
```

### Option 2: Homebrew (macOS/Linux)

```bash
# Add the tap
brew tap ciroarendt/codrsync

# Install codrsync
brew install codrsync

# Verify installation
codrsync --version
```

### Option 3: pip

```bash
pip install codrsync
codrsync --version
```

### Option 4: pipx (Isolated Environment)

```bash
pipx install codrsync
codrsync --version
```

### Option 5: npm

```bash
npm install -g codrsync
codrsync --version
```

## Configuration

### API Key Setup

For AI-powered features, set one of these API keys:

```bash
# Anthropic (Claude) - Recommended
export ANTHROPIC_API_KEY="sk-ant-..."

# OpenAI (GPT)
export OPENAI_API_KEY="sk-..."

# Google (Gemini)
export GOOGLE_API_KEY="..."
```

Add this to your `~/.bashrc` or `~/.zshrc` for persistence.

### Cloud Authentication

Alternatively, use codrsync cloud (includes API access):

```bash
codrsync auth --cloud
```

This opens a browser for authentication.

### Check Configuration

```bash
codrsync doctor
```

## Your First Project

### New Project

```bash
# Create and enter project directory
mkdir my-project && cd my-project

# Initialize with codrsync
codrsync init
```

The wizard will guide you through:
1. Project name and description
2. Language/framework selection
3. Initial structure creation
4. PRP (Product Requirement Prompt) generation

### Existing Project

```bash
cd your-existing-project

# Scan to detect stack
codrsync scan

# Connect integrations
codrsync connect

# Check status
codrsync status
```

### Superego Mode (with Claude Code)

Use codrsync as a meta-orchestrator for Claude Code:

```bash
codrsync start
```

This launches Claude Code with codrsync context and guidelines.

## Project Structure

After initialization, codrsync creates:

```
your-project/
├── doc/
│   ├── project/
│   │   ├── context.md      # Project context for AI
│   │   └── scan-result.json
│   ├── prp/
│   │   └── *.md            # Product Requirement Prompts
│   └── task/
│       └── context-session.md
├── CLAUDE.md               # Claude Code instructions
└── ... your code
```

## Next Steps

- [CLI Commands Reference](cli/commands.md)
- [Quickstart Guide](guides/quickstart.md)
- [Integration Setup](guides/integrations.md)
