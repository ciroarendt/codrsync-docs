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

Alternativamente, use codrsync cloud (inclui acesso à API):

```bash
codrsync auth --cloud
```

Isso abre o navegador para autenticação.

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
- [Configuração de Integrações](guides/integrations.md)
