# codrsync

**Turn any dev into jedi ninja codr**

codrsync is an AI-powered development orchestrator that helps you ship faster with confidence through guided implementation, interactive validation, and persistent context.

## Features

- **AI-Guided Development**: Intelligent assistance for complex implementations
- **Project Scaffolding**: Quick project setup with best practices
- **Stack Detection**: Automatic detection of languages, frameworks, and tools
- **Integration Support**: Connect with Supabase, Vercel, GitHub, and more
- **Persistent Context**: Maintains project context across sessions

## Installation

### Via Homebrew (macOS)

```bash
brew tap ciroarendt/codrsync
brew install codrsync
```

### Via pip

```bash
pip install codrsync
```

## Quick Start

```bash
# Initialize a new project
codrsync init

# Scan existing project
codrsync scan

# Check project status
codrsync status

# Connect integrations
codrsync connect
```

## Documentation

- [Getting Started](docs/getting-started.md)
- [CLI Commands](docs/cli/commands.md)
- [Guides](docs/guides/)

## Configuration

Set your Anthropic API key for AI features:

```bash
export ANTHROPIC_API_KEY="your-key"
```

Or login to codrsync cloud:

```bash
codrsync auth --cloud
```

## Links

- [Website](https://codrsync.dev)
- [PyPI](https://pypi.org/project/codrsync/)
- [Homebrew Tap](https://github.com/ciroarendt/homebrew-codrsync)

## License

MIT
