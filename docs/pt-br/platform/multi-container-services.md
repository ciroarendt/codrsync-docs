---
title: Workspaces Multi-Container e Serviços
description: Como rodar serviços sidecar (Redis, Postgres, n8n, etc.) no seu workspace, com DNS automático e TLS.
order: 10
---

# Workspaces Multi-Container e Serviços

## O Que São Serviços Sidecar?

Um workspace codrsync é mais que um editor de código — é um container Linux completo com rede Docker, URL pública e TLS. Serviços sidecar permitem adicionar containers extras (Redis, Postgres, n8n, RabbitMQ, Evolution API e mais) que rodam ao lado do seu workspace na mesma rede.

Quando o Titan cria um sidecar, ele roda como container Docker na mesma rede interna do workspace. Seu código acessa pelo hostname (ex: `ws-seuslug-redis:6379`). Se expor o serviço, ele ganha um subdomínio HTTPS automático como `redis-seuslug.app.codrsync.dev`.

## Templates de Serviço Disponíveis

| Serviço | Imagem | Porta | RAM Padrão | Caso de Uso |
|---------|--------|-------|------------|-------------|
| **redis** | redis:7-alpine | 6379 | 128 MB | Cache, message broker, sessões, filas |
| **postgres** | postgres:16-alpine | 5432 | 256 MB | Banco relacional para dados estruturados |
| **n8n** | n8nio/n8n:latest | 5678 | 512 MB | Automação visual de workflows (tipo Zapier) |
| **rabbitmq** | rabbitmq:3-management-alpine | 5672 | 256 MB | Fila de mensagens avançada |
| **evolution-api** | atendai/evolution-api:latest | 8080 | 512 MB | WhatsApp Business API |
| **minio** | minio/minio:latest | 9000 | 256 MB | Object storage S3-compatível local |
| **qdrant** | qdrant/qdrant:latest | 6333 | 256 MB | Banco vetorial para IA/embeddings |

## Como Usar Serviços Sidecar

Peça ao Titan naturalmente:

- "Adiciona Redis ao meu workspace"
- "Preciso de um banco Postgres com senha minhasenha123"
- "Configura n8n com URL pública para receber webhooks"
- "Cria um stack de prospecção: Redis + Postgres + Evolution API"

O Titan usa a ferramenta `service_create` para provisionar o container, configurar a rede e opcionalmente expor com subdomínio HTTPS público.

### Ferramentas do Titan para Gerenciar Serviços

- **service_templates** — Lista todos os serviços disponíveis e suas specs
- **service_create** — Cria um novo sidecar (nome, variáveis de ambiente, se expõe publicamente)
- **service_list** — Mostra todos os sidecars rodando com suas URLs
- **service_remove** — Para e remove um sidecar
- **service_logs** — Ver logs recentes de um sidecar

## Limites por Plano

| Plano | Max Sidecars | Max RAM Sidecars | Max Expostos (URL pública) |
|-------|-------------|-----------------|---------------------------|
| Basic (free/pro) | 0 | 0 | 0 |
| Pro (pro_plus/team) | 3 | 1 GB total | 2 |
| Power (enterprise) | 8 | 4 GB total | 5 |

Usuários no plano Basic não podem criar sidecars. Faça upgrade para Pro ou Power para liberar.

## Rede Entre Serviços

Todos os sidecars compartilham a mesma rede Docker do workspace. Acesse qualquer sidecar pelo hostname do container:

```python
# Python — conectando ao Redis sidecar
import redis
r = redis.Redis(host='ws-seuslug-redis', port=6379)
r.set('chave', 'valor')
```

```javascript
// Node.js — conectando ao Postgres sidecar
const { Pool } = require('pg');
const pool = new Pool({
  host: 'ws-seuslug-postgres',
  port: 5432,
  user: 'postgres',
  password: 'minhasenha',
  database: 'postgres',
});
```

O Titan sabe os hostnames exatos e vai configurar seu código corretamente.

## URLs Públicas e DNS

Ao expor um sidecar, ele recebe subdomínio HTTPS automático:

```
{servico}-{workspace-slug}.app.codrsync.dev
```

Exemplo: `n8n-c0e0e0b7f.app.codrsync.dev`

URL acessível publicamente com certificado TLS válido (Let's Encrypt). Perfeito para:
- **Endpoints de webhook** — receber callbacks do Stripe, WhatsApp, GitHub, etc.
- **Endpoints de API** — expor FastAPI ou Express para a internet
- **Dashboards admin** — acessar n8n, gerenciamento do RabbitMQ, console do MinIO

## Ciclo de Vida: O Que Acontece Quando Seu Workspace Pausa?

Quando o workspace auto-pausa por inatividade:

1. Todos os containers sidecar são **parados**
2. Volumes de dados são **arquivados no cloud storage** (Storj) — libera disco local
3. URLs públicas são **desregistradas** (retornam 404 até resumir)

Ao resumir o workspace:

1. Volumes são **restaurados do cloud storage** (~10-30 segundos extras)
2. Containers sidecar são **recriados** com a mesma configuração
3. URLs públicas são **re-registradas** com TLS
4. **Todos os seus dados estão intactos** — nada é perdido

Isso significa que você não gasta recursos quando não está usando, mas tudo volta exatamente como deixou.

## Arquitetura de Storage

O codrsync usa três camadas de storage, otimizadas para custo e performance:

| Camada | Onde | Velocidade | Custo | Usado Para |
|--------|------|-----------|-------|-----------|
| **Hot** | SSD local | <1ms | Incluído | Dados ativos dos sidecars (tabelas Postgres, chaves Redis) |
| **Warm** | Storj (S3) | ~50-100ms | ~$7/TB/mês | Uploads de apps, PDFs, imagens (via cloud-gateway) |
| **Cold** | Storj (S3) | ~5-30s | ~$4/TB/mês | Archives de volumes (automático ao pausar) |

Seu código pode usar o cloud-gateway como API S3-compatível para armazenar arquivos:

```python
import requests

# Upload de arquivo para cloud storage (de dentro do workspace)
requests.put(
    'http://cloud-gateway:3003/s3/meu-bucket/foto.jpg',
    headers={'Authorization': f'Bearer {INTERNAL_TOKEN}'},
    data=open('foto.jpg', 'rb'),
)
```

Útil para uploads de usuários, relatórios gerados, backups ou qualquer dado que deve persistir independente do estado do workspace.

## Casos de Uso Comuns

### Máquina de Prospecção Automatizada
Setup típico para automação de geração de leads:
- **n8n** (exposto): Orquestração de workflows — scraping de leads, enriquecimento, sequência de outreach
- **Postgres**: Armazenar dados de leads, rastrear estágios do pipeline
- **Redis**: Cache de perfis enriquecidos, gerenciar rate limits
- **Evolution API** (exposto): Outreach via WhatsApp por webhook

Peça ao Titan: "Monte um stack de prospecção com n8n, Postgres, Redis e Evolution API. Exponha n8n e Evolution API publicamente."

### Backend SaaS
Rode todo seu backend:
- **Postgres**: Banco principal
- **Redis**: Store de sessões + cache
- **RabbitMQ**: Fila de jobs background
- Sua app **FastAPI/Express** rodando no workspace

### Pipeline IA/ML
Processar e buscar embeddings:
- **Qdrant**: Banco vetorial para busca semântica
- **Postgres**: Metadata e dados de usuários
- **Redis**: Cache de respostas de API
- **MinIO**: Armazenar dados de treino e artefatos de modelo

### Bot WhatsApp
Automatizar conversas WhatsApp:
- **Evolution API** (exposto): Receber e enviar mensagens WhatsApp
- **n8n** (exposto): Builder visual de workflows para lógica de conversa
- **Redis**: Estado de sessão para conversas multi-turno
- **Postgres**: Log de mensagens e analytics

## Comparação com Publicação Estática (CDN)

O codrsync oferece duas formas de "publicar" do workspace:

| Feature | CDN Estático (existente) | Serviços Sidecar (novo) |
|---------|-------------------------|------------------------|
| O que serve | Arquivos HTML, CSS, JS | Processos rodando |
| Sobrevive a pausa? | Sim (arquivos no Storj) | Dados sim, processos não (restart ao resumir) |
| Precisa compute? | Não (Storj serve) | Sim (containers rodando) |
| Formato da URL | cdn.codrsync.dev/s/slug/ | servico-slug.app.codrsync.dev |
| Melhor para | Landing pages, docs, SPAs | APIs, bots, automação, bancos de dados |

Publicação estática é ótima para front-end. Serviços sidecar são para qualquer coisa que precisa de um processo rodando — bancos, APIs, bots, motores de workflow.

## Notas de Segurança

- Apenas imagens de container pré-aprovadas são permitidas (sem imagens Docker arbitrárias)
- Variáveis de ambiente dos sidecars (senhas, API keys) são armazenadas encriptadas e nunca mostradas no chat
- Serviços são bloqueados em modo review (Titan Review) e modo planejamento
- Limites de recursos são aplicados por plano — não é possível exceder a cota de RAM/serviços
- Cada serviço roda com limites de CPU e memória para prevenir esgotamento de recursos
