# Referência de Comandos CLI

## Opções Globais

```bash
codrsync [OPÇÕES] COMANDO [ARGS]
```

| Opção | Descrição |
|-------|-----------|
| `--version`, `-v` | Mostrar versão e sair |
| `--help` | Mostrar mensagem de ajuda |
| `--help-ai` | Iniciar chat de onboarding com IA |
| `--lang [en\|pt-br]` | Definir idioma |

---

## Comandos Locais (Sem IA)

### status

Mostrar dashboard de status do projeto.

```bash
codrsync status [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |

---

### roadmap

Mostrar roadmap e timeline do projeto.

```bash
codrsync roadmap
```

---

### export

Exportar projeto para diferentes formatos.

```bash
codrsync export [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--format FORMATO` | Formato de saída: `json`, `markdown`, `excel`, `jira`, `trello`, `notion` |
| `--output CAMINHO` | Caminho do arquivo de saída |

**Exemplos:**
```bash
codrsync export --format excel --output relatorio-sprint.xlsx
codrsync export --format jira
codrsync export --format notion
```

---

### scan

Escanear projeto atual para detectar stack, docs e integrações.

```bash
codrsync scan [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto (padrão: atual) |
| `--github` | Importar issues e PRs do GitHub |
| `--docs` | Escanear arquivos de documentação |
| `--deep` | Gerar resumo de contexto com IA |

**Exemplo:**
```bash
codrsync scan --github --docs
```

**Detecta:**
- Linguagens: Python, JavaScript/TypeScript, Go, Rust, etc.
- Frameworks: Next.js, FastAPI, Django, Express, etc.
- Bancos de dados: Prisma, Supabase, PostgreSQL, MongoDB
- Infraestrutura: Docker, Kubernetes, Vercel, GitHub Actions
- Ferramentas: Tailwind CSS, ESLint, Prettier, etc.

---

### connect

Verificar e mostrar status de integrações com serviços externos.

```bash
codrsync connect [SERVIÇO] [OPÇÕES]
```

| Serviço | Descrição |
|---------|-----------|
| `supabase` | Conectar projeto Supabase |
| `vercel` | Conectar deploy Vercel |
| `github` | Conectar repositório GitHub |
| `tailwind` | Detectar configuração Tailwind |
| `mcp` | Detectar servidores MCP |
| `digitalocean` | Conectar DigitalOcean |

**Exemplo:**
```bash
codrsync connect           # Todos os serviços
codrsync connect supabase  # Serviço específico
```

---

### sprint

Gerenciar sprints de desenvolvimento.

```bash
codrsync sprint [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `start` | Iniciar nova sprint |
| `plan` | Planejar tarefas e metas da sprint |
| `review` | Revisar progresso da sprint |
| `retro` | Executar retrospectiva da sprint |
| `close` | Fechar sprint atual |
| `check` | Verificar saúde da sprint |
| `time` | Mostrar rastreamento de tempo |
| `calibrate` | Calibrar estimativas de velocidade |
| `list` | Listar todas as sprints |
| `current` | Mostrar sprint atual |
| `create` | Criar nova sprint |

**Exemplos:**
```bash
codrsync sprint start --name "Sprint 5"
codrsync sprint plan
codrsync sprint check
codrsync sprint review
codrsync sprint retro
codrsync sprint close
codrsync sprint calibrate
```

---

## Comandos com IA

### init

Inicializar novo projeto com kickstart guiado por IA.

```bash
codrsync init [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto (padrão: atual) |
| `--template NOME` | Usar um template específico |

**Exemplo:**
```bash
codrsync init --path ./meu-app
```

Se executado em diretório com código existente, oferece importar o projeto.

---

### build

Executar desenvolvimento com guia de IA.

```bash
codrsync build [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--prp ARQUIVO` | Arquivo PRP para executar |
| `--step N` | Iniciar de passo específico |

---

### prp

Gerenciar PRPs (Product Requirement Prompts).

```bash
codrsync prp [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `list` | Listar todos os PRPs |
| `create` | Criar novo PRP |
| `show NOME` | Mostrar detalhes do PRP |

---

### start

Iniciar Claude Code com codrsync como superego.

```bash
codrsync start [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--path CAMINHO` | Diretório do projeto |
| `--model MODELO` | Modelo de IA a usar |

Inicia o Claude Code com contexto completo do projeto e diretrizes do codrsync.

---

### docrsync

Gerar documentação técnica do seu codebase.

```bash
codrsync docrsync [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--mode MODO` | Modo de geração: `readme`, `technical`, `full` |
| `--output CAMINHO` | Diretório de saída |

**Custo em créditos:**

| Modo | Descrição | Créditos |
|------|-----------|----------|
| `readme` | Gerar arquivo README | 5 |
| `technical` | ~10 páginas de documentação | 15 |
| `full` | Suite completa de documentação | 30 |

**Exemplos:**
```bash
codrsync docrsync --mode readme          # 5 créditos
codrsync docrsync --mode technical       # 15 créditos
codrsync docrsync --mode full            # 30 créditos
```

**Disponível em:** Pro, Pro+, Teams.

---

### pptrsync

Criar apresentações do seu codebase com IA.

```bash
codrsync pptrsync [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--mode MODO` | Modo de geração: `quick`, `standard`, `full` |
| `--flux` | Usar imagens Flux Pro (somente Pro+) |
| `--output CAMINHO` | Caminho do arquivo de saída |

**Custo em créditos:**

| Modo | Slides | Créditos |
|------|--------|----------|
| `quick` | 5 slides | 10 |
| `standard` | 10 slides | 20 |
| `full` | 20 slides | 35 |
| `--flux` | Imagens Flux Pro | +10 |

**Exemplos:**
```bash
codrsync pptrsync --mode quick           # 10 créditos
codrsync pptrsync --mode standard        # 20 créditos
codrsync pptrsync --mode full --flux     # 45 créditos
codrsync export --format pptx            # Exportar para PPTX (+5 créditos)
```

**Disponível em:** Pro, Pro+, Teams.

---

### envrsync

Analisar o ambiente do seu projeto.

```bash
codrsync envrsync [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--deep` | Executar análise profunda com IA (5 créditos) |

**Custo em créditos:**

| Modo | Descrição | Créditos |
|------|-----------|----------|
| Padrão | Scan básico local | 0 (grátis) |
| `--deep` | Análise completa com IA | 5 |

**Exemplos:**
```bash
codrsync envrsync                        # Scan básico (grátis)
codrsync envrsync --deep                 # Análise profunda com IA (5 créditos)
```

**Disponível em:** Todos os planos. Análise profunda requer Pro+.

---

## Comandos de Armazenamento Cloud

### storage

Gerenciar armazenamento cloud cloudrsync. [Docs completos do cloudrsync →](../products/cloudrsync.md)

```bash
codrsync storage [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `init` | Inicializar conexão de armazenamento cloud |
| `put <local> <remoto>` | Upload de arquivo para cloud |
| `get <remoto> <local>` | Download de arquivo da cloud |
| `ls [bucket]` | Listar buckets ou arquivos em um bucket |
| `rm <remoto>` | Remover arquivo da cloud |
| `config` | Mostrar configuração de armazenamento |

**Exemplos:**
```bash
codrsync storage init
codrsync storage put ./dados.csv meu-bucket/dados.csv
codrsync storage get meu-bucket/dados.csv ./dados-local.csv
codrsync storage ls
codrsync storage ls meu-bucket
codrsync storage rm meu-bucket/arquivo-antigo.txt
codrsync storage config
```

### storage bucket

Gerenciar buckets de armazenamento.

```bash
codrsync storage bucket [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `create <nome> [--backend storj\|filecoin]` | Criar novo bucket |
| `list` | Listar todos os buckets |
| `delete <nome>` | Excluir um bucket |

**Exemplos:**
```bash
codrsync storage bucket create meu-bucket                    # Storj (padrão)
codrsync storage bucket create meu-arquivo --backend filecoin  # Filecoin
codrsync storage bucket list
codrsync storage bucket delete bucket-antigo
```

### storage keys

Gerenciar chaves API compatíveis com S3.

```bash
codrsync storage keys [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `create --name <nome>` | Criar nova chave API |
| `list` | Listar todas as chaves API |
| `revoke <key-id>` | Revogar uma chave API |

**Exemplos:**
```bash
codrsync storage keys create --name "produção"
codrsync storage keys list
codrsync storage keys revoke abc123
```

---

## Comandos de Sessão Cloud

### cloud

Gerenciar sessões do workspace cloud.

```bash
codrsync cloud [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `status` | Mostrar status do workspace cloud |
| `download` | Baixar arquivos do workspace |
| `upload` | Upload de arquivos para workspace |
| `stop` | Parar workspace cloud |

---

## Comandos de Faturamento

### billing

Gerenciar assinatura e faturamento.

```bash
codrsync billing [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `status` | Mostrar plano atual e uso |
| `upgrade` | Abrir portal de upgrade |
| `portal` | Abrir portal de faturamento Stripe |
| `credits` | Mostrar saldo de créditos |

### credits

Gerenciar créditos.

```bash
codrsync credits [SUBCOMANDO]
```

| Subcomando | Descrição |
|------------|-----------|
| `buy` | Comprar créditos adicionais ($5/100) |
| `history` | Ver histórico de uso de créditos |

---

## Comandos de Configuração

### auth

Configurar autenticação.

```bash
codrsync auth [OPÇÕES]
```

| Opção | Descrição |
|-------|-----------|
| `--cloud` | Autenticar com codrsync cloud |
| `--logout` | Remover credenciais salvas |
| `--status` | Mostrar status de autenticação |

---

### doctor

Verificar instalação e configuração do codrsync.

```bash
codrsync doctor [OPÇÕES]
```

Verifica:
- Versão do Python
- Configuração da chave API
- Estrutura do projeto
- Status das integrações
- Dependências do CLI

---

## Códigos de Saída

| Código | Significado |
|--------|-------------|
| 0 | Sucesso |
| 1 | Erro geral |
| 2 | Erro de configuração |
| 3 | Autenticação necessária |
