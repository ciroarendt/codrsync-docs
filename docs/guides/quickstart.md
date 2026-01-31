# Quickstart Guide

Get up and running with codrsync in 5 minutes.

## 1. Install

```bash
# macOS
brew tap ciroarendt/codrsync && brew install codrsync

# or via pip
pip install codrsync
```

## 2. Configure API Key

```bash
export ANTHROPIC_API_KEY="your-key"
```

## 3. Create Your First Project

```bash
mkdir my-app && cd my-app
codrsync init
```

Follow the interactive prompts to:
- Name your project
- Choose language/framework
- Set up initial structure

## 4. Explore Commands

```bash
# Check project status
codrsync status

# Run diagnostics
codrsync doctor

# Start AI session
codrsync kickstart
```

## 5. For Existing Projects

```bash
cd your-project

# Detect stack
codrsync scan

# Connect services
codrsync connect
```

## What's Next?

- [Full CLI Reference](../cli/commands.md)
- [Integration Setup](integrations.md)
- [Best Practices](best-practices.md)

## Need Help?

- [Website](https://codrsync.dev)
- [Documentation](https://codrsync.dev/docs)
