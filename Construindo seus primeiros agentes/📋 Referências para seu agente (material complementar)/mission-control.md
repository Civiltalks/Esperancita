---
name: mission-control
status: ATIVO
category: cheatsheet
referenced_by: [A14]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra construir um Mission Control customizado — dashboard visual com Kanban, conteúdo, métricas, ideias de mercado, gestão de agentes. Workflow do Bruno (template + audit segurança + PRD via superpowers + iteração via Telegram). 4 prompts prontos pra colar.
---

# Mission Control — referência rápida (A14)

## O que é Mission Control

Mission Control = **dashboard visual customizado** que você constrói pra ter visão de cockpit dos seus negócios + agentes em uma tela só.

Diferente da observabilidade nativa do OpenClaw (CLI status/health, dashboard web Hostinger), Mission Control é **camada de cima** — visualização integrada com:

- Kanban estilo Trello (tarefas dos agentes)
- Área de conteúdo (criar, agendar, publicar redes sociais)
- Métricas de redes sociais (via Apify ou APIs nativas)
- Pesquisa de mercado / trends / ideias de conteúdo
- Integração Notion (gestão de projetos cruzada)
- Dashboard SaaS (faturamento, churn, MRR)
- Gestão de bosses/agentes (gancho A13)

**Tese central**: você não precisa observar tudo via Telegram. Mission Control é o lugar onde **você vê a empresa toda em uma tela** — e cada card aciona o agente certo.

## Workflow do Bruno (9 etapas)

### Etapa 1 — Achar template-base no GitHub

> *"Pesquise pra mim os top 5 Mission Control / dashboards open-source no GitHub. Foco em: visual atraente, fácil de customizar, stack Next.js + Supabase. Me lista 5 com prós/contras."*

Bruno usou: **TenacityOS** (Carlos Azaustre) — template TS/Next.js com escritório 3D, Kanban, painéis.

### Etapa 2 — Audit de segurança no template

> *"Vou usar este template: [link do GitHub]. Antes de eu clonar, faz audit de segurança: prompt injections, malware, vulnerabilidades, dependências sketchy."*

### Etapa 3 — Montar PRD com fixes de segurança

> *"Beleza. Agora monta um PRD pra eu construir esse Mission Control. Inclui: resumo, mapeamento da minha infra, fixes de segurança, fases de implementação, must-have vs nice-to-have."*

### Etapa 4 — Instalar skill `superpowers`

```bash
openclaw skills install superpowers
```

Skill superpowers traz 3 capacidades centrais:
- **Brainstorming** — agente pergunta antes de construir
- **Writing-plans** — agente quebra projeto em tasks pequenas
- **Executing-plans** — agente executa plano passo a passo + audit

### Etapa 5 — Re-revisar PRD com superpowers

> *"Use o brainstorming + writing-plans do superpowers pra revisar o PRD. Me faz as perguntas críticas que faltaram. Define must-have vs nice-to-have."*

### Etapa 6 — Definir branding

> *"Define o branding baseado em: meu USER.md, minha empresa principal, paleta visual que combine. Cores, tipografia, tom de copy. Me apresenta 2-3 opções."*

### Etapa 7 — Construir fundação

**Caminho A — Aluno Managed:**
> *"Executa o PRD na minha estrutura OpenClaw. Use a skill superpowers (executing-plans). Cada chunk verifica se funciona antes de avançar."*

Custo estimado: 1-2h · gasto significativo de tokens (preferir Sonnet pra economia).

**Caminho B — Aluno VPS standalone:**
- Cloud Code SSH na VPS
- Executa PRD via Cloud Code (mais barato em tokens)

### Etapa 8 — QA agent pós-construção

> *"Audit de QA: revisa cada arquivo, valida que tudo funciona, lista pendências, identifica bugs."*

### Etapa 9 — Iterar via Telegram com áudio

Daqui em diante, refinamento via Telegram (áudio ou texto).

## Hospedagem do dashboard

| Perfil | Caminho recomendado | Custo mensal |
|--------|---------------------|--------------|
| **PME Managed (curso default)** | Vercel (Next.js) + Supabase free | R$ 0 |
| **PME Managed avançado** | Hostinger free hosting + Supabase | R$ 0 |
| **Dev/avançado** | VPS Hostinger + Tailscale + Supabase self-hosted | R$ 30-50 |
| **Enterprise** | Cloudflare Pages + Supabase Pro + custom domain | R$ 80-200 |

**Princípio**: comece grátis. Migre quando provar que vale.

## Multi-agente como produto deste workflow

Mission Control é **prova viva de multi-agente em ação** (gancho A13). Cada card pode acionar um agente diferente:

| Card | Agente que aciona | Papel |
|------|-------------------|-------|
| Coordenação geral | Agente principal (Cosa Mora) | Chief of Staff |
| Conteúdo | Agente especializado (FLG Amora) | Produção de conteúdo |
| Métrica/SaaS | Agente operacional (MGM Amora) | Gestão SaaS |
| Pra equipe | Agente de equipe (Leonardo Da Vinci) | Compartilhado entre sócios |
| Comunidade | Agente cliente-facing (openclawzinho) | WhatsApp 24/7 |

## 4 prompts prontos pra colar

### 1. Pesquisar template Mission Control

```
Pesquise pra mim os top 5 Mission Control / dashboards open-source
no GitHub que sirvam como base pra eu construir o meu. Foco em:
- Visual atraente
- Stack acessível (Next.js + Supabase OU equivalente)
- Fácil de customizar
- Documentação razoável
- Última atualização <12 meses

Me lista 5 com nome, link, stack, prós/contras, complexidade pra
customizar e recomendação.
```

### 2. Audit de segurança no template escolhido

```
Vou usar este template: [URL do GitHub]

Antes de eu clonar, faz audit de segurança completo:

1. Lê o código realmente — package.json, scripts, API routes, env handling
2. Identifica:
   - Prompt injections em prompts hardcoded
   - Malware ou backdoor (suspicious imports, shell exec)
   - Vulnerabilidades em dependências
   - Credenciais expostas em commits
   - Tokens hardcoded em código
3. Me dá relatório com classificação: CRÍTICO / ALTO / MÉDIO / BAIXO
4. Pra cada issue, sugere fix concreto

Se achar algo CRÍTICO, PARA e me pergunta antes de continuar.
```

### 3. Montar PRD do Mission Control

```
Beleza, validamos a segurança. Agora monta o PRD.

Estrutura:
1. Resumo executivo
2. Mapeamento da minha infra (lê meu workspace, AGENTS.md, .env)
3. Fixes dos problemas de segurança identificados
4. Fases de implementação (mínimo 4 chunks)
5. Must-have vs Nice-to-have
6. Estimativa de tempo + tokens
7. Pendências e decisões

Use a skill superpowers (writing-plans) pra estruturar.
Front-end primeiro, back-end depois.
```

### 4. Iteração via Telegram (uso contínuo)

```
[áudio ou texto]:

"Mora, no Mission Control:
- O card de campanha não tem subtasks. Adiciona campo pra subtasks.
- Quero marcar qual agente vai executar cada task.
- Dashboard de métricas — adiciona filtro por período.
- Bug: quando arrasto card pra 'done', a contagem não atualiza.

Faz tudo, manda print, espera confirmação antes de deployar."
```

## Stack opcional — métricas de redes sociais

| Serviço | Uso | Custo |
|---------|-----|-------|
| **Apify** | Scraping (Instagram, LinkedIn, TikTok) | US$ 30-40/mês |
| **APIs gratuitas** | LinkedIn API · Instagram Graph · YouTube Data | R$ 0 |
| **Skill `social-metrics-collect`** | Combina APIs gratuitas | R$ 0 |

**Princípio**: métricas é **nice-to-have** no MVP. Foca em Kanban + conteúdo + integração Notion primeiro.

## Princípios de segurança aplicados (recap A10)

1. **Audit de segurança ANTES de clonar template**
2. **Tokens com scope mínimo**
3. **Hospedagem privada** — repo no GitHub privado · Supabase com RLS · Vercel com env protection
4. **Defesa anti-prompt-injection** (Mission Control lê inputs externos)
5. **Cap de custo por agente** que opera Mission Control
6. **Backup do código** — repo Git · snapshot Hostinger periódico

## Quando NÃO construir Mission Control

- **Aluno PME no day 1-30**: stay com Telegram + observabilidade nativa
- **1 agente único, sem multi-agente**: pode esperar
- **Sem volume de tarefas**: Kanban com 5 cards/dia não justifica
- **Sem budget pra hospedagem nem API**: pular

## Caveats Managed vs VPS

A aula original do Bruno mostra workflow com **Cloud Code SSH na VPS Hostinger**. Aluno do curso (Managed) tem 2 caminhos:

**Caminho A — Tudo via agente OpenClaw Managed (default):**
- Funciona — só vai gastar mais do plano OpenAI/Anthropic
- Sem necessidade de VPS · sem Cloud Code · sem Tailscale

**Caminho B — Aluno avançado com VPS (gancho R1-R4 bônus):**
- Mais barato em tokens · mais setup inicial

## Referências

- A14 · A8 (skills) · A10 (segurança) · A12 (integrações) · A13 (multi-agente)
- TenacityOS: https://github.com/azaustre/tenacityos
- Vercel: https://vercel.com · Supabase: https://supabase.com

---

📌 Atualizado em 04/05/2026 · Pixel Educação
