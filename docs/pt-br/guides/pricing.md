# Preços & Planos

## Planos

### Grátis — $0 para sempre

Perfeito para experimentar e projetos open source.

- Funcionalidade completa do CLI
- Metodologia Context Engineering
- BYOK obrigatório (traga sua própria chave API)
- Scans básicos envrsync
- cloudrsync: 1 GB armazenamento + 5 GB egress/mês
- Suporte comunitário

### Pro — $29/mês

Para desenvolvedores solo e freelancers. Trial gratuito de 14 dias, sem cartão de crédito.

- Tudo do Grátis
- Cloud Workspace incluído
- 500 créditos/mês
- Documentação docrsync
- Apresentações pptrsync
- Análise profunda envrsync com IA
- cloudrsync: 50 GB armazenamento + 100 GB egress/mês
- Suporte prioritário

### Pro+ — $49/mês

Para power users e pequenas empresas. Trial gratuito de 14 dias.

- Tudo do Pro
- 1.500 créditos/mês
- pptrsync com imagens Flux Pro
- Domínio personalizado para workspace
- Rollover de créditos (até 500 créditos)
- cloudrsync: 200 GB armazenamento + 500 GB egress/mês
- Suporte prioritário

### Teams — $99/vaga/mês

Para equipes de desenvolvimento. Mínimo 3 vagas.

- Tudo do Pro+
- 2.000 créditos/vaga/mês
- Auto-documentação contínua (docrsync)
- Dashboard de admin e analytics
- Integração SSO/SAML
- SLA 99.9%
- Limites cloudrsync personalizados
- Suporte dedicado

---

## Matriz de Recursos

| Recurso | Grátis | Pro | Pro+ | Teams |
|---------|--------|-----|------|-------|
| **codrsync CLI** | Completo | Completo | Completo | Completo |
| **BYOK** | Sim | Sim | Sim | Sim |
| **Cloud Workspace** | — | Sim | Sim | Sim |
| **docrsync** | — | Sim | Sim | Auto-updates |
| **pptrsync** | — | Sim | + Flux Pro | + Flux Pro |
| **envrsync básico** | Sim | Sim | Sim | Sim |
| **envrsync profundo** | — | Sim | Sim | Sim |
| **cloudrsync armazenamento** | 1 GB | 50 GB | 200 GB | Personalizado |
| **cloudrsync egress** | 5 GB/mês | 100 GB/mês | 500 GB/mês | Personalizado |
| **Backend Filecoin** | — | Sim | Sim | Sim |
| **Créditos/mês** | 0 | 500 | 1.500 | 2.000/vaga |
| **Rollover de créditos** | — | — | 500 máx | 500 máx |
| **Domínio personalizado** | — | — | Sim | Sim |
| **SSO/SAML** | — | — | — | Sim |
| **SLA** | — | — | — | 99.9% |
| **Suporte** | Comunitário | Prioritário | Prioritário | Dedicado |

---

## Custos em Créditos

Créditos são usados por docrsync, pptrsync e envrsync. cloudrsync usa limites de armazenamento do plano, não créditos.

### docrsync

| Modo | Resultado | Créditos |
|------|-----------|----------|
| README | Arquivo README único | 5 |
| Técnico | ~10 páginas de documentação | 15 |
| Suite completa | Pacote completo de docs | 30 |

### pptrsync

| Modo | Resultado | Créditos |
|------|-----------|----------|
| Quick deck | 5 slides | 10 |
| Standard deck | 10 slides | 20 |
| Full deck | 20 slides | 35 |
| Imagens Flux Pro | Visuais premium com IA | +10 |
| Exportação PPTX/PDF | Arquivo para download | +5 |

### envrsync

| Modo | Resultado | Créditos |
|------|-----------|----------|
| Scan básico | Análise local | 0 (grátis) |
| Análise profunda com IA | Relatório completo com IA | 5 |

### Créditos Extras

- **$5 por 100 créditos** — Compre a qualquer momento
- Válidos em todos os produtos
- Plano Pro+ inclui rollover de até 500 créditos não utilizados/mês

---

## Preços de Armazenamento Cloud

Custos de armazenamento estão incluídos nos limites do plano. Para referência, as taxas por TB:

### Backend Storj (Recomendado)

| | Taxa |
|---|---|
| Armazenamento | $7/TB/mês |
| Egress | $12/TB/mês |

### Backend Filecoin (Verificável)

| | Taxa |
|---|---|
| Armazenamento | $30/TB/mês |
| Egress | $30/TB/mês |

### Comparação com Grandes Provedores (10 TB/ano)

| Provedor | Custo Anual |
|----------|-------------|
| **cloudrsync (Storj)** | **~$840** |
| cloudrsync (Filecoin) | ~$3.600 |
| AWS S3 | ~$3.730 |
| Google Cloud Storage | ~$3.714 |
| Azure Blob | ~$3.294 |

---

## FAQ

**Posso usar codrsync de graça?**
Sim. O plano Grátis é permanente — CLI completo com BYOK, scans básicos envrsync e 1 GB de armazenamento cloud.

**O que é BYOK?**
Bring Your Own Key (Traga Sua Própria Chave). Use suas próprias chaves API (Anthropic, OpenAI, Google) em qualquer plano. O plano Grátis requer BYOK.

**Créditos expiram?**
Créditos são resetados mensalmente. Planos Pro+ e Teams podem fazer rollover de até 500 créditos não utilizados.

**Posso experimentar o Pro antes de pagar?**
Sim. Pro e Pro+ incluem trial gratuito de 14 dias, sem cartão de crédito.

**O que acontece se eu exceder os limites de armazenamento?**
Você precisará fazer upgrade do plano ou remover arquivos para ficar dentro dos limites.

---

## Veja Também

- [Visão Geral dos Produtos](../products/suite-overview.md)
- [Documentação cloudrsync](../products/cloudrsync.md)
- [Guia do Dashboard](dashboard.md)
