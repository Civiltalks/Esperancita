# Case Filippe César — 3 empresas com CoS coordenando

> Empreendedor sócio em 3 empresas. Tem 1 agente por empresa + 1 Chief of Staff coordenando os 3. Arquitetura multiempresa real.

---

## Quem opera

**Filippe César** · empreendedor · sócio em 3 empresas distintas (setores diferentes).

Cada empresa tem operação, equipe e contexto próprios. Filippe precisa estar presente em todas mas é uma pessoa só.

---

## A arquitetura

**1 agente por empresa + 1 CoS:**

```
                  ┌─────────────────────┐
                  │  CoS (no Telegram)  │
                  │  Coordenador geral  │
                  └──────────┬──────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
          ┌───▼───┐      ┌───▼───┐      ┌───▼───┐
          │Agente │      │Agente │      │Agente │
          │Empresa│      │Empresa│      │Empresa│
          │   A   │      │   B   │      │   C   │
          └───────┘      └───────┘      └───────┘
```

### CoS (Chief of Staff)
- Roda no Telegram pessoal do Filippe
- Recebe relatórios diários de cada agente
- Roteia tarefas: "isso é da empresa A, manda pro agente A"
- Mantém visão consolidada das 3 operações

### Agente por empresa
- Cada um com **cérebro/memória própria por contexto**
- SOUL/IDENTITY/USER independentes
- Não compartilha credenciais nem contexto entre empresas
- Reporta apenas pro CoS, não pros outros agentes

---

## Como cooperam

Comunicação é via:

1. **Reports diários:** cada agente envia digest 18h pro CoS
2. **Arquivos compartilhados:** decisões cross-empresa em `shared/decisoes/`
3. **CoS roteia manualmente:** Filippe fala com CoS, CoS decide qual agente acionar

**Princípio crítico:** agentes de empresas diferentes **não conversam direto**. Sempre passam pelo CoS pra evitar vazamento de contexto e leak entre operações.

---

## Stack

- **VPS standalone** com 3 OpenClaws (1 por empresa) + 1 OpenClaw separado pro CoS
- **Canais:** Telegram (CoS) + Slack das empresas + Discord interno
- **Modelo:** Claude Sonnet 4.5 nos agentes + Claude Opus 4.6 no CoS (raciocínio mais profundo)
- **Crons:** ~15 por empresa (relatórios, alertas, monitoramento financeiro)
- **Integrações:** Notion (cada empresa tem workspace), GitHub privado, Stripe (financeiro), Calendar

---

## Resultado mensurável

- **Tempo poupado:** ~30h/semana — Filippe não precisa estar mentalmente em 3 empresas o tempo todo
- **Decisões cross-empresa:** consolidadas pelo CoS (antes ele perdia oportunidades de sinergia)
- **Custo:** ~R$ 1.800/mês (4 agentes + VPS robusta + integrações)
- **ROI:** ~10x (sócio que opera 3 empresas vale muito mais sendo presente nas 3)

---

## Lições replicáveis

### O que QUALQUER aluno pode aplicar

1. **CoS coordenador é padrão poderoso** — empreendedor com 2+ negócios deveria ter
2. **Escopo restrito é fundamental** — agentes de empresas diferentes **NÃO** se veem
3. **Reports diários são a cola** — sem digest 18h pro CoS, ele perde contexto
4. **Modelo top no CoS, modelo médio nos agentes** — economia: ~70% custo do mesmo setup all-Opus

### Quando aplicar

- Você é sócio em 2+ empresas distintas
- Operações têm contextos completamente diferentes (não só "marketing" + "vendas" da mesma empresa — isso é 1 agente com 2 skills)
- Você esquece de fazer follow-ups cross-empresa
- Já tem volume real (multi-agente em fase de teste = overengineering)

### Quando NÃO aplicar

- Você opera 1 empresa só (1 agente bem feito resolve)
- Empresas pequenas demais sem volume de operação real
- Você ainda não consolidou 1 agente — não pula etapas

---

## Frase do Filippe

> "Eu era 1 cabeça operando 3 empresas mal. Hoje sou 1 humano + 4 agentes operando 3 empresas bem."

---

## Onde ver mais

- Cheatsheet `multi-agente.md` (na pasta Cheatsheets) — Prompt #5 e #6 cobrem agente paralelo dedicado a canal
- Aula A13 da Hotmart aprofunda
- Template AGENTS.md mostra como configurar organograma multi-empresa

---

📌 Atualizado em 04/05/2026 · Pixel Educação
