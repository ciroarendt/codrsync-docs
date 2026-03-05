---
title: Insights de Arquitetura da Plataforma
description: Insights estratégicos sobre a evolução do codrsync de workspace para mini-PaaS, tiers de storage e estratégia de escala.
order: 11
---

# Insights de Arquitetura da Plataforma

## codrsync Já É uma VPS

Um workspace codrsync não é apenas uma IDE no browser. É um container Linux completo rodando em servidor ARM Hetzner com:
- Rede Docker (bridge compartilhada com todos os serviços da plataforma)
- URL pública com TLS (via Traefik reverse proxy)
- Volumes persistentes (sobrevivem pause/resume)
- Acesso direto a cloud storage (Storj via cloud-gateway)
- Assistente de desenvolvimento com IA (Titan)

Isso significa que o codrsync já fornece a infraestrutura que usuários tipicamente precisam de uma VPS. A evolução chave é permitir que usuários rodem stacks multi-container — não apenas um container de workspace.

## De Arquivos Estáticos a Processos Rodando

O codrsync tem dois modelos de publicação:

**Publicação Estática (CDN):** Arquivos do workspace são exportados, enviados ao Storj e servidos via `cdn.codrsync.dev`. O workspace pode pausar — arquivos persistem no Storj. Ideal para landing pages, sites de documentação, SPAs e portfólios.

**Publicação de Serviços (Sidecars):** Containers adicionais rodam ao lado do workspace com URLs HTTPS públicas. São processos rodando — bancos de dados, APIs, bots, motores de workflow. Precisam de compute (CPU/RAM) e seus dados são arquivados no Storj quando o workspace pausa.

O gap entre esses dois é o gap entre "hospedar um site" e "rodar infraestrutura." Serviços sidecar preenchem esse gap.

## Estratégia de Tiers de Storage

A plataforma usa três camadas de storage para balancear performance e custo:

**Tier hot (SSD, <1ms):** Volumes Docker para containers sidecar ativos. Dados do Postgres, AOF do Redis, bancos do n8n. Limitado pela capacidade SSD do servidor (320 GB no servidor atual). Usado apenas quando containers estão ativamente rodando.

**Tier warm (Storj, ~50-100ms):** Blobs de aplicação acessados via API S3 do cloud-gateway. Uploads de usuários, PDFs gerados, imagens, exports. Capacidade ilimitada a ~$7/TB/mês. Apps dentro do workspace usam `http://cloud-gateway:3003/s3/` como endpoint S3 — sem necessidade de credenciais.

**Tier cold (archive Storj, ~5-30s):** Volumes de sidecar arquivados. Quando workspace pausa, volumes de dados são comprimidos (tar.gz) e enviados ao Storj, liberando SSD local. No resume, são baixados e restaurados. Workspaces pausados custam essencialmente $0 em recursos do servidor.

Futuro: Filecoin via Storacha (PRP-22) adicionará tier ultra-cold a ~$3/TB/mês para archives de longo prazo (volumes pausados >30 dias).

## Sem MinIO na Arquitetura

O cloud-gateway conecta diretamente ao endpoint S3-compatível do Storj usando AWS SDK v3. Não há MinIO intermediário. O próprio cloud-gateway atua como proxy S3 autenticado — containers de workspace chamam com INTERNAL_TOKEN e ele encaminha para o Storj.

Para usuários que precisam de API S3 local (ex: app que espera endpoint S3), MinIO pode ser adicionado como sidecar opcional. Mas para a maioria dos casos, o cloud-gateway é suficiente e mais simples.

## Arquitetura de DNS e Roteamento

Todo roteamento passa pelo Traefik v3.3 usando file provider (não Docker provider, que está quebrado no Docker Engine 29.x).

**Rotas de workspace:** `{slug}.ws.codrsync.dev` → `ws-{slug}:8080` via arquivos YAML por workspace em `/etc/traefik/dynamic/`.

**Rotas de serviço:** `{nome}-{slug}.app.codrsync.dev` → `ws-{slug}-{nome}:{porta}` via arquivos YAML por serviço.

**Rotas estáticas:** `cdn.codrsync.dev`, `n8n.codrsync.dev` → containers backend fixos.

Certificados TLS são emitidos por hostname via Let's Encrypt HTTP-01. DNS wildcard (`*.ws.codrsync.dev`, `*.app.codrsync.dev`) resolve todos os subdomínios para o IP do servidor, e Traefik roteia pelo header Host.

## Caminho de Escala

**Servidor atual (Hetzner CAX41):** 16 ARM vCPU, 32 GB RAM, 320 GB SSD (~€27/mês). Suporta ~25 stacks de workspace concorrentes com sidecars.

**Primeira escala:** Adicionar worker node (CAX31, ~€14/mês). Manager roda no nó primário, containers de workspace rodam no worker. O manager já usa dockerode — trocar de socket local para Docker host remoto é mudança mínima de código.

**Multi-node:** Docker Swarm ou k3s com 2+ worker nodes. Traefik fica no nó primário como ingress controller.

A estratégia de cold storage (archive no Storj ao pausar) significa que capacidade de disco é necessária apenas para stacks ativamente rodando, tornando o servidor muito mais eficiente.

## Integração n8n (PRP-81)

Existe uma instância compartilhada do n8n em `n8n.codrsync.dev` que todos os workspaces podem usar via ferramentas MCP (n8n_ping, n8n_execute, etc.). É para automações e ações da plataforma (criar issues GitHub, enviar mensagens Telegram, etc.).

Com serviços sidecar do PRP-82, usuários também podem rodar sua PRÓPRIA instância do n8n como sidecar, totalmente sob seu controle. O n8n compartilhado é para ações da plataforma codrsync; o n8n per-user é para automações específicas do usuário.

## Insight Chave: Usuários de Automação Precisam de Stacks, Não Só Código

O usuário tradicional de "workspace de código" quer escrever e rodar código. Mas usuários focados em automação (agências, times de growth, empreendedores solo) precisam de uma proposta de valor diferente:

- **Precisam de infraestrutura rodando**, não apenas um ambiente de desenvolvimento
- **Precisam de endpoints de webhook** para receber callbacks de serviços externos
- **Precisam de bancos de dados** para persistir estado entre execuções de workflow
- **Precisam de filas de mensagens** para processamento assíncrono confiável
- **Precisam de processos always-on** (bots, scrapers, servidores de API)

Serviços sidecar transformam o codrsync de "lugar para escrever código" em "lugar para rodar todo o seu stack de automação." O assistente IA (Titan) torna isso acessível para usuários não-DevOps — eles descrevem o que querem, e o Titan provisiona a infraestrutura.
