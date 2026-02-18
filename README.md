# codrsync

[English](#english) | [Português](#português)

---

## English

**AI Development Orchestrator + Product Suite**

codrsync is an AI-powered development orchestrator and product suite that helps you ship faster with confidence. From context engineering and guided implementation to cloud storage, auto-documentation, and AI presentations — everything you need to build, document, and deploy.

### Product Suite

| Product | Description | Availability |
|---------|-------------|--------------|
| [**codrsync**](docs/en/products/suite-overview.md#codrsync) | AI development orchestrator with context engineering | Free + All Plans |
| [**cloudrsync**](docs/en/products/cloudrsync.md) | S3-compatible cloud storage — up to 70% cheaper than AWS | Free (1 GB) / Pro+ |
| [**docrsync**](docs/en/products/suite-overview.md#docrsync) | Auto-generate and maintain technical documentation | Pro+ |
| [**pptrsync**](docs/en/products/suite-overview.md#pptrsync) | Create presentations from your codebase with AI visuals | Pro+ |
| [**envrsync**](docs/en/products/suite-overview.md#envrsync) | Environment scanner — stack detection, security analysis | Free (basic) / Pro |

> **Coming soon:** [gpursync](docs/en/products/suite-overview.md#gpursync) — Distributed GPU cloud for ML workloads.

### Installation

```bash
# Recommended: Install script
curl -fsSL https://codrsync.dev/install.sh | bash

# Homebrew (macOS/Linux)
brew tap ciroarendt/codrsync
brew install codrsync

# pip
pip install codrsync

# pipx (isolated environment)
pipx install codrsync

# npm (installs Python package automatically)
npm install -g codrsync
```

### Quick Start

```bash
# Initialize a new project
codrsync init

# Scan existing project
codrsync scan

# Start superego mode with Claude Code
codrsync start

# Set up cloud storage
codrsync storage init

# Login to codrsync cloud
codrsync auth --cloud
```

### Documentation

- [Getting Started](docs/en/getting-started.md)
- [CLI Commands](docs/en/cli/commands.md)
- [Quickstart Guide](docs/en/guides/quickstart.md)
- [Product Suite Overview](docs/en/products/suite-overview.md)
- [cloudrsync (Cloud Storage)](docs/en/products/cloudrsync.md)
- [Pricing & Plans](docs/en/guides/pricing.md)
- [Dashboard Guide](docs/en/guides/dashboard.md)

### Configuration

```bash
# Anthropic (Claude)
export ANTHROPIC_API_KEY="your-key"

# OpenAI (GPT)
export OPENAI_API_KEY="your-key"

# Or login to codrsync cloud
codrsync auth --cloud
```

---

## Português

**Orquestrador de Desenvolvimento com IA + Suite de Produtos**

codrsync é um orquestrador de desenvolvimento com IA e suite de produtos que ajuda você a entregar mais rápido e com confiança. De engenharia de contexto e implementação guiada a armazenamento cloud, documentação automática e apresentações com IA — tudo que você precisa para construir, documentar e fazer deploy.

### Suite de Produtos

| Produto | Descrição | Disponibilidade |
|---------|-----------|-----------------|
| [**codrsync**](docs/pt-br/products/suite-overview.md#codrsync) | Orquestrador de desenvolvimento com IA e engenharia de contexto | Grátis + Todos os Planos |
| [**cloudrsync**](docs/pt-br/products/cloudrsync.md) | Armazenamento cloud compatível com S3 — até 70% mais barato que AWS | Grátis (1 GB) / Pro+ |
| [**docrsync**](docs/pt-br/products/suite-overview.md#docrsync) | Gere e mantenha documentação técnica automaticamente | Pro+ |
| [**pptrsync**](docs/pt-br/products/suite-overview.md#pptrsync) | Crie apresentações do seu código com visuais gerados por IA | Pro+ |
| [**envrsync**](docs/pt-br/products/suite-overview.md#envrsync) | Scanner de ambiente — detecção de stack, análise de segurança | Grátis (básico) / Pro |

> **Em breve:** [gpursync](docs/pt-br/products/suite-overview.md#gpursync) — GPU cloud distribuída para cargas de trabalho ML.

### Instalação

```bash
# Recomendado: Script de instalação
curl -fsSL https://codrsync.dev/install.sh | bash

# Homebrew (macOS/Linux)
brew tap ciroarendt/codrsync
brew install codrsync

# pip
pip install codrsync

# pipx (ambiente isolado)
pipx install codrsync

# npm (instala o pacote Python automaticamente)
npm install -g codrsync
```

### Início Rápido

```bash
# Inicializar novo projeto
codrsync init

# Escanear projeto existente
codrsync scan

# Iniciar modo superego com Claude Code
codrsync start

# Configurar armazenamento cloud
codrsync storage init

# Login no codrsync cloud
codrsync auth --cloud
```

### Documentação

- [Primeiros Passos](docs/pt-br/getting-started.md)
- [Comandos CLI](docs/pt-br/cli/commands.md)
- [Guia Rápido](docs/pt-br/guides/quickstart.md)
- [Visão Geral dos Produtos](docs/pt-br/products/suite-overview.md)
- [cloudrsync (Cloud Storage)](docs/pt-br/products/cloudrsync.md)
- [Preços & Planos](docs/pt-br/guides/pricing.md)
- [Guia do Dashboard](docs/pt-br/guides/dashboard.md)

### Configuração

```bash
# Anthropic (Claude)
export ANTHROPIC_API_KEY="sua-chave"

# OpenAI (GPT)
export OPENAI_API_KEY="sua-chave"

# Ou faça login no codrsync cloud
codrsync auth --cloud
```

---

## Links

- [Website](https://codrsync.dev)
- [PyPI](https://pypi.org/project/codrsync/)
- [npm](https://www.npmjs.com/package/codrsync)
- [Homebrew Tap](https://github.com/ciroarendt/homebrew-codrsync)

## License / Licença

MIT
