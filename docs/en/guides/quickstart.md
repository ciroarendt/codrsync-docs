# Quickstart Guide

Get up and running with codrsync in 5 minutes.

## 1. Install

```bash
# macOS/Linux
brew tap ciroarendt/codrsync && brew install codrsync

# or via pip
pip install codrsync
```

## 2. Configure API Key

```bash
# Use your own key (BYOK)
export ANTHROPIC_API_KEY="your-key"

# Or login to codrsync cloud for full features
codrsync auth --cloud
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

# Start superego mode with Claude Code
codrsync start
```

## 5. For Existing Projects

```bash
cd your-project

# Detect stack
codrsync scan

# Connect services
codrsync connect
```

## 6. Try Cloud Storage

```bash
# Initialize cloud storage
codrsync storage init

# Create a bucket (AES-256-GCM encrypted by default)
codrsync storage bucket create my-data

# Upload a file
codrsync storage put ./report.csv my-data/report.csv

# List files
codrsync storage ls my-data

# Download
codrsync storage get my-data/report.csv ./downloaded.csv
```

Free plan includes 1 GB of storage. [Upgrade](pricing.md) for up to 200 GB.

## What's Next?

- [Full CLI Reference](../cli/commands.md) — All commands and options
- [Product Suite Overview](../products/suite-overview.md) — codrsync, cloudrsync, docrsync, pptrsync, envrsync
- [cloudrsync Documentation](../products/cloudrsync.md) — Cloud storage deep dive
- [Pricing & Plans](pricing.md) — Plans, credits, and storage limits
- [Dashboard Guide](dashboard.md) — Manage everything from the web

## Need Help?

- [Website](https://codrsync.dev)
- [Documentation](https://codrsync.dev/docs)
