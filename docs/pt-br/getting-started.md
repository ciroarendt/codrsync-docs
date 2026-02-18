# Primeiros Passos

## Pré-requisitos

- Python 3.10 ou superior
- Um dos: pip, pipx, Homebrew ou npm
- Chave API para recursos de IA (Anthropic, OpenAI ou codrsync cloud)

## Instalação

### Opção 1: Script de Instalação (Recomendado)

```bash
curl -fsSL https://codrsync.dev/install.sh | bash
```

### Opção 2: Homebrew (macOS/Linux)

```bash
# Adicionar o tap
brew tap ciroarendt/codrsync

# Instalar codrsync
brew install codrsync

# Verificar instalação
codrsync --version
```

### Opção 3: pip

```bash
pip install codrsync
codrsync --version
```

### Opção 4: pipx (Ambiente Isolado)

```bash
pipx install codrsync
codrsync --version
```

### Opção 5: npm

```bash
npm install -g codrsync
codrsync --version
```

## Configuração

### Configuração de Chave API

Para recursos com IA, configure uma dessas chaves API:

```bash
# Anthropic (Claude) - Recomendado
export ANTHROPIC_API_KEY="sk-ant-..."

# OpenAI (GPT)
export OPENAI_API_KEY="sk-..."

# Google (Gemini)
export GOOGLE_API_KEY="..."
```

Adicione ao seu `~/.bashrc` ou `~/.zshrc` para persistir.

### Autenticação Cloud

Alternativamente, use codrsync cloud (inclui acesso à API, armazenamento cloud e créditos):

```bash
codrsync auth --cloud
```

Isso abre o navegador para autenticação. Com uma conta cloud você também tem acesso ao [armazenamento cloudrsync](products/cloudrsync.md), ao [dashboard web](guides/dashboard.md) e recursos como docrsync e pptrsync dependendo do seu plano.

### Verificar Configuração

```bash
codrsync doctor
```

## Seu Primeiro Projeto

### Novo Projeto

```bash
# Criar e entrar no diretório do projeto
mkdir meu-projeto && cd meu-projeto

# Inicializar com codrsync
codrsync init
```

O wizard vai guiá-lo através de:
1. Nome e descrição do projeto
2. Seleção de linguagem/framework
3. Criação da estrutura inicial
4. Geração de PRP (Product Requirement Prompt)

### Projeto Existente

```bash
cd seu-projeto-existente

# Escanear para detectar stack
codrsync scan

# Conectar integrações
codrsync connect

# Verificar status
codrsync status
```

### Modo Superego (com Claude Code)

Use codrsync como meta-orquestrador para Claude Code:

```bash
codrsync start
```

Isso inicia o Claude Code com contexto e diretrizes do codrsync.

## Configuração de Armazenamento Cloud

Configure o cloudrsync para armazenar arquivos em armazenamento cloud criptografado:

```bash
# Login no codrsync cloud
codrsync auth --cloud

# Inicializar armazenamento
codrsync storage init

# Criar seu primeiro bucket
codrsync storage bucket create meu-bucket

# Upload de arquivo
codrsync storage put ./meuarquivo.txt meu-bucket/meuarquivo.txt
```

Todos os buckets usam criptografia AES-256-GCM por padrão. Veja a [documentação do cloudrsync](products/cloudrsync.md) para detalhes completos incluindo configuração de cliente S3.

## A Suite de Produtos

codrsync é mais do que um CLI — é uma plataforma completa de desenvolvimento:

| Produto | O que faz |
|---------|-----------|
| **codrsync** | Orquestrador de desenvolvimento com IA e engenharia de contexto |
| **cloudrsync** | Armazenamento cloud compatível com S3 (Storj + Filecoin) |
| **docrsync** | Gere documentação técnica automaticamente |
| **pptrsync** | Crie apresentações do seu codebase |
| **envrsync** | Scanner de ambiente e análise de segurança |

Veja a [Visão Geral dos Produtos](products/suite-overview.md) para detalhes de cada produto.

## Estrutura do Projeto

Após inicialização, codrsync cria:

```
seu-projeto/
├── doc/
│   ├── project/
│   │   ├── context.md      # Contexto do projeto para IA
│   │   └── scan-result.json
│   ├── prp/
│   │   └── *.md            # Product Requirement Prompts
│   └── task/
│       └── context-session.md
├── CLAUDE.md               # Instruções para Claude Code
└── ... seu código
```

## Próximos Passos

- [Referência de Comandos CLI](cli/commands.md)
- [Guia Rápido](guides/quickstart.md)
- [Visão Geral dos Produtos](products/suite-overview.md)
- [cloudrsync (Cloud Storage)](products/cloudrsync.md)
- [Preços & Planos](guides/pricing.md)
- [Guia do Dashboard](guides/dashboard.md)
