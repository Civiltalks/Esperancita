# Case Igor Gouveia — Time multiagente para agência

> Time de 5 agentes especializados rodando 24/7 em infra própria. Referência de multi-agente real.

---

## Quem opera

**Igor Gouveia** · agência de IA + e-commerce (Shopify focused).

Atende clientes em produção: criação de loja, gestão de campanhas, atendimento, suporte técnico, email marketing.

---

## O time multiagente

5 agentes com função clara, cada um com SOUL/IDENTITY próprios:

### 🎨 DaVinci — Estrategista
- Define direção criativa de campanha
- Cria briefings pros outros agentes
- Coordena entregas

### 🎬 Scarlett — Criativo
- Gera copy de anúncio
- Roteiro de vídeo
- Layouts de criativos
- Adapta tom por canal/cliente

### 🛠️ Cyber — Técnico
- Implementa landing page
- Configura integrações
- Resolve bugs em código
- Setup de tracking

### 📧 Alecto — Email
- Sequências de nurturing
- Automação de carrinho abandonado
- Re-engagement
- A/B test de subject lines

### 🛒 Titan — Shopify
- Configura loja
- Gerencia produtos · variantes · estoque
- Integra apps
- Otimiza conversão

---

## Como cooperam

Não é DM direta. Igor (humano) orquestra via:

- **Mention em canal compartilhado:** `@DaVinci @Scarlett briefing pro cliente X`
- **Arquivos compartilhados:** DaVinci escreve briefing em `shared/briefings/`, Scarlett lê quando precisa
- **Subagente spawn:** Cyber dispara subagente de pesquisa quando precisa de doc técnica externa

Cada agente tem **escopo restrito** — Scarlett não tem acesso a credenciais Shopify (só Titan), Alecto não vê briefings estratégicos (só DaVinci e Scarlett).

---

## Stack

- **VPS standalone** (não Managed) — múltiplos OpenClaws na mesma VPS
- **Canais:** Telegram (DM Igor + 5 tópicos · 1 por agente), Discord (cliente), Slack (equipe)
- **Modelo:** Claude Sonnet 4.5 (econômico) + Opus 4.6 (DaVinci só, pra raciocínio profundo)
- **Crons:** ~30 ativos (relatórios diários por cliente, monitoramento de campanha, alertas de Stripe)
- **Skills custom:** dezenas (briefing-cliente, gerar-criativo, audit-shopify, sequencia-email, etc.)

---

## Resultado mensurável

- **Tempo poupado:** ~50h/semana (Igor + 1 assistente fazem trabalho de equipe de 4-5 pessoas)
- **Volume de cliente:** 3x mais clientes por mesmo headcount
- **Custo total da operação:** ~R$ 1.500/mês (5 agentes + VPS + Apify)
- **ROI:** 15-20x

---

## Lições replicáveis

### O que QUALQUER aluno pode aplicar

1. **Multi-agente faz sentido pra agência/serviço** — domínios distintos (criativo · técnico · email · loja) = agentes distintos
2. **Cada agente com SOUL próprio** — DaVinci é direto, Scarlett é poética, Cyber é técnico
3. **Escopo restrito é segurança** — Scarlett não tem acesso a credencial sensível
4. **VPS é pra quem opera multi-agente sério** — Managed limita a 1 OpenClaw por plano

### Cuidados

- **Multi-agente é refinamento, não default** — Igor evoluiu pra 5 agentes em meses, não no dia 1
- **3 agentes ≠ 3x trabalho** — mais perto de 5x manutenção (SOULs + USERs + credenciais + monitoramento)
- **Não cria agente por estética** — cada agente precisa de domínio claro e volume real

---

## Onde ver mais

- Cheatsheet `multi-agente.md` (na pasta Cheatsheets) cobre os 4 caminhos de comunicação
- Template `AGENTS.md` na pasta Templates documenta como organizar organograma
- Aula A13 da Hotmart aprofunda multi-agente

---

📌 Atualizado em 04/05/2026 · Pixel Educação
