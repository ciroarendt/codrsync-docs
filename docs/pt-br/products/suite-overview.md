# Visão Geral dos Produtos

codrsync é mais do que um CLI — é uma plataforma completa de desenvolvimento. Aqui está tudo na suite.

## codrsync

**Orquestrador de Desenvolvimento com IA**

O CLI principal que orquestra seu desenvolvimento com IA. Engenharia de contexto que torna qualquer IA 10x mais inteligente.

- **Suporte universal a IA** — Claude, GPT-5, Gemini 3, Grok, ou modelos locais via Ollama
- **Contexto persistente** — O conhecimento do seu projeto sobrevive entre sessões
- **Validação superego** — Use codrsync como meta-orquestrador para Claude Code
- **Integrações MCP** — Conecte Supabase, Vercel, GitHub e mais
- **BYOK suportado** — Traga sua própria chave API em qualquer plano

```bash
codrsync init        # Inicializar projeto
codrsync scan        # Detectar stack e integrações
codrsync start       # Iniciar modo superego
codrsync build       # Desenvolvimento guiado por IA
```

**Disponível em:** Todos os planos (Grátis inclui CLI completo com BYOK).

---

## cloudrsync

**Armazenamento Cloud Compatível com S3**

Armazenamento cloud em uma rede global distribuída — até 70% mais barato que AWS S3 com criptografia AES-256-GCM por padrão.

- **Dois backends** — Storj (recomendado, $7/TB) ou Filecoin (verificável, $30/TB)
- **API compatível com S3** — Funciona com AWS CLI, boto3, qualquer SDK S3
- **Criptografia zero-knowledge** — AES-256-GCM habilitada em todos os buckets
- **99.9999999% durabilidade** — Confiabilidade enterprise
- **Sem vendor lock-in** — Protocolo S3 padrão

**Armazenamento por plano:** Grátis 1 GB / Pro 50 GB / Pro+ 200 GB

[Documentação completa do cloudrsync →](cloudrsync.md)

---

## docrsync

**Documentação Automática**

Gere e mantenha documentação técnica automaticamente. README, docs de API, guias — sempre atualizados.

- **Docs auto-gerados** — A partir da análise do codebase
- **Documentação de API** — Compatível com OpenAPI/Swagger
- **Suporte multi-idioma** — Inglês, Português e mais
- **Atualizações contínuas** — Plano Teams inclui auto-updates contínuos

### Custo em Créditos

| Modo | Resultado | Créditos |
|------|-----------|----------|
| README | Arquivo README único | 5 |
| Docs técnicos | ~10 páginas de documentação | 15 |
| Suite completa | Pacote completo de documentação | 30 |

```bash
codrsync docrsync --mode readme       # 5 créditos
codrsync docrsync --mode technical    # 15 créditos
codrsync docrsync --mode full         # 30 créditos
```

**Disponível em:** Pro, Pro+, Teams. Não disponível no Grátis.

---

## pptrsync

**Apresentações com IA**

Crie apresentações bonitas do seu codebase. Pitch decks, demos, relatórios com visuais gerados por IA.

- **Geração de slides com IA** — Analise código e crie slides automaticamente
- **Imagens Flux Pro** — Visuais premium gerados por IA (somente Pro+)
- **Exportação PPTX/PDF** — Download em formatos padrão
- **Templates personalizados** — Combine com sua marca

### Custo em Créditos

| Modo | Resultado | Créditos |
|------|-----------|----------|
| Quick deck | 5 slides | 10 |
| Standard deck | 10 slides | 20 |
| Full deck | 20 slides | 35 |
| Imagens Flux Pro | Imagens premium geradas por IA | +10 |
| Exportação PPTX/PDF | Arquivo para download | +5 |

```bash
codrsync pptrsync --mode quick        # 10 créditos
codrsync pptrsync --mode standard     # 20 créditos
codrsync pptrsync --mode full         # 35 créditos
codrsync pptrsync --mode full --flux  # 45 créditos (full + Flux Pro)
codrsync export --format pptx         # +5 créditos
```

**Disponível em:** Pro, Pro+, Teams. Não disponível no Grátis.

---

## envrsync

**Scanner de Ambiente**

Analise o ambiente do seu projeto instantaneamente. Detecte stack, dependências, problemas de segurança e receba recomendações com IA.

- **Detecção de stack** — Linguagens, frameworks, bancos de dados, ferramentas
- **Análise de segurança** — Varredura de vulnerabilidades e recomendações
- **Auditoria de dependências** — Pacotes desatualizados, problemas de licença
- **Recomendações com IA** — Sugestões de melhoria acionáveis

### Custo em Créditos

| Modo | Descrição | Créditos |
|------|-----------|----------|
| Scan básico | Análise local, sem IA | 0 (grátis) |
| Análise profunda com IA | Análise completa com IA | 5 |

```bash
codrsync envrsync                    # Scan básico (grátis)
codrsync envrsync --deep             # Análise profunda com IA (5 créditos)
```

**Disponível em:** Todos os planos. Grátis inclui scans básicos; Pro+ inclui análise profunda com IA.

---

## gpursync

**GPU Cloud Distribuída** *(Em Breve)*

Computação GPU sob demanda para treinamento ML, inferência e processamento em lote — alimentado por uma rede distribuída de provedores GPU.

- **GPUs sob demanda** — Sem compromissos de longo prazo
- **Rede distribuída** — Acesse GPUs globalmente
- **Otimizado para ML** — Pré-configurado para TensorFlow, PyTorch, JAX
- **Custo-eficiente** — Pague apenas pelo que usar

> gpursync está atualmente em desenvolvimento. [Entre na lista de espera →](https://codrsync.dev/gpursync)

---

## Comparação de Planos

| Recurso | Grátis | Pro ($29/mês) | Pro+ ($49/mês) | Teams ($99/vaga/mês) |
|---------|--------|---------------|----------------|----------------------|
| codrsync CLI | Completo | Completo | Completo | Completo |
| Cloud Workspace | — | Incluído | Incluído | Incluído |
| cloudrsync storage | 1 GB | 50 GB | 200 GB | Personalizado |
| docrsync | — | 5-30 créditos | 5-30 créditos | Auto-updates |
| pptrsync | — | 10-35 créditos | + Flux Pro | + Flux Pro |
| envrsync | Básico | + IA Profunda | + IA Profunda | + IA Profunda |
| Créditos/mês | 0 | 500 | 1.500 | 2.000/vaga |
| Rollover de créditos | — | — | Até 500 | Até 500 |

[Detalhes completos de preços →](../guides/pricing.md)
