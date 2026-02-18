# Guia Rápido

Comece a usar o codrsync em 5 minutos.

## 1. Instalar

```bash
# macOS/Linux
brew tap ciroarendt/codrsync && brew install codrsync

# ou via pip
pip install codrsync
```

## 2. Configurar Chave API

```bash
# Use sua própria chave (BYOK)
export ANTHROPIC_API_KEY="sua-chave"

# Ou faça login no codrsync cloud para recursos completos
codrsync auth --cloud
```

## 3. Criar Seu Primeiro Projeto

```bash
mkdir meu-app && cd meu-app
codrsync init
```

Siga os prompts interativos para:
- Nomear seu projeto
- Escolher linguagem/framework
- Configurar estrutura inicial

## 4. Explorar Comandos

```bash
# Verificar status do projeto
codrsync status

# Executar diagnósticos
codrsync doctor

# Iniciar modo superego com Claude Code
codrsync start
```

## 5. Para Projetos Existentes

```bash
cd seu-projeto

# Detectar stack
codrsync scan

# Conectar serviços
codrsync connect
```

## 6. Experimentar Armazenamento Cloud

```bash
# Inicializar armazenamento cloud
codrsync storage init

# Criar um bucket (criptografia AES-256-GCM por padrão)
codrsync storage bucket create meus-dados

# Upload de arquivo
codrsync storage put ./relatorio.csv meus-dados/relatorio.csv

# Listar arquivos
codrsync storage ls meus-dados

# Download
codrsync storage get meus-dados/relatorio.csv ./baixado.csv
```

O plano Grátis inclui 1 GB de armazenamento. [Faça upgrade](pricing.md) para até 200 GB.

## Próximos Passos

- [Referência Completa CLI](../cli/commands.md) — Todos os comandos e opções
- [Visão Geral dos Produtos](../products/suite-overview.md) — codrsync, cloudrsync, docrsync, pptrsync, envrsync
- [Documentação cloudrsync](../products/cloudrsync.md) — Deep dive em armazenamento cloud
- [Preços & Planos](pricing.md) — Planos, créditos e limites de armazenamento
- [Guia do Dashboard](dashboard.md) — Gerencie tudo pelo navegador

## Precisa de Ajuda?

- [Website](https://codrsync.dev)
- [Documentação](https://codrsync.dev/docs)
