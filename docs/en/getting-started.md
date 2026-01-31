# Getting Started

## Prerequisites

- Python 3.10 or higher
- pip or Homebrew (for installation)
- Anthropic API key (for AI features)

## Installation

### Option 1: Homebrew (Recommended for macOS)

```bash
# Add the tap
brew tap ciroarendt/codrsync

# Install codrsync
brew install codrsync

# Verify installation
codrsync --version
```

### Option 2: pip

```bash
pip install codrsync
codrsync --version
```

## Configuration

### API Key Setup

For AI-powered features, you need an Anthropic API key:

```bash
export ANTHROPIC_API_KEY="sk-ant-..."
```

Add this to your `~/.bashrc` or `~/.zshrc` for persistence.

### Cloud Authentication

Alternatively, use codrsync cloud:

```bash
codrsync auth --cloud
```

This opens a browser for authentication.

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

### Existing Project

```bash
cd your-existing-project

# Scan to detect stack
codrsync scan

# Connect integrations
codrsync connect
```

## Next Steps

- [CLI Commands Reference](cli/commands.md)
- [Quickstart Guide](guides/quickstart.md)
- [Integration Setup](guides/integrations.md)
