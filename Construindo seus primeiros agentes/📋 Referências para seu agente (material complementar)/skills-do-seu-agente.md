---
name: skills-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A8]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra skills do agente OpenClaw (A8). Cobre conceito skill vs prompt · 8 capacidades nativas · tour das 6 skills curadas · anatomia do SKILL.md · criação custom via criar-skill · 3 fontes oficiais · 5 prompts prontos.
---

# Skills do seu agente — referência rápida (A8)

## A8 em 1 minuto (resumo executivo)

Skill = **SOP executável nomeado** que o agente carrega quando o gatilho dispara. Diferente de prompt (one-shot), skill executa os mesmos passos, retorna o mesmo formato, todo dia.

| Conceito | O que é | Exemplo |
|----------|---------|---------|
| **Prompt** | Instrução one-shot | "Resume essas 3 dúvidas pra mim agora" |
| **Skill** | Capacidade que vira hábito do agente | `relatorio-comunidade-semanal` roda toda sexta automaticamente |
| **Capacidade nativa** | Tool que já vem de fábrica | Agente já lê PDF e gera imagem sem instalar nada |

**Frase-mãe da A8:** *"prompt resolve uma vez. Skill resolve mil vezes igual."*

## Skill vs prompt — quando virar skill

Cria skill quando:
1. Você pediu a mesma tarefa **2+ vezes** (3+ é certeza)
2. O **formato de saída** importa
3. Você quer combinar com **cron** depois (A9)
4. Tarefa só faz sentido **no seu sistema**

Não cria skill quando:
- Tarefa pontual que não vai repetir
- Pergunta de pesquisa one-shot
- Job que tool nativa já faz sozinha

## Capacidades nativas — bateria recheada

Em ~80% dos casos, tool nativa já resolve.

| Capacidade | O que faz | Quando usar |
|------------|-----------|-------------|
| **PDF** | Lê, extrai texto/tabelas, gera novos | Resumo de contrato · proposta |
| **Browser** | Abre site, navega, extrai conteúdo | Pesquisa concorrência |
| **Web search** | 12 providers nativos | Notícia · validar fato |
| **Image-gen** | Gera imagem (DALL-E e outros) | Capa de post · ilustração |
| **TTS** | Texto vira áudio | Briefing em áudio |
| **Memória semântica** | Embeddings + busca | Recall de decisão antiga (A7) |
| **Cron** | Agendamento nativo (A9) | Health check · revisão do dia |
| **ClawHub** | App store oficial | Skill pronta sem clonar repo |

## Tour das 6 skills curadas

| Skill | Origem | Pra que serve |
|-------|--------|---------------|
| **using-superpowers** | Comunidade | Wrapper meta-skill: brainstorm → PRD → execute |
| **criar-skill** | Bruno | A skill que cria skill |
| **skill-checkup-openclaw** | Bruno (v1.3.0) | Diagnóstico executivo do agente · score 0-100 |
| **canvas-design** | Anthropic | Gera poster, capa, ilustração estática |
| **last30days** | Comunidade | Pesquisa profunda dos últimos 30 dias |
| **pptx** | Anthropic | Gera apresentação `.pptx` completa em 1 prompt |

## Anatomia mínima do SKILL.md

| Seção | Pra que serve | Exemplo |
|-------|---------------|---------|
| **1. Nome (frontmatter)** | Identificador único | `name: relatorio-comunidade-semanal` |
| **2. Descrição/propósito** | 1-2 frases — o que faz e quando usar | "Toda sexta agrupa dúvidas do Telegram" |
| **3. Trigger (inputs)** | Frases que disparam | "Quando eu mandar link Tella" |
| **4. Runbook (passos)** | Sequência ordenada | "1. Lê últimos 7d. 2. Agrupa. 3. Salva." |
| **5. Output esperado** | Formato de saída padronizado | "HTML usando template `report-comunidade.html`" |

## 5 prompts prontos pra colar

### 1. Listar skills atuais e detectar as não-usadas

```
Lista todas as skills instaladas no meu workspace.

Pra cada uma me diz:
1. Nome + descrição em 1 linha
2. Última vez que rodou (se tiver registro)
3. Se eu usei nos últimos 30 dias

No final, sugere quais posso desinstalar sem culpa
(skill que não rodou em 30+ dias provavelmente não encaixou).

Não desinstala nada — só me mostra a lista pra eu decidir.
```

### 2. Criar skill custom baseada em rotina repetitiva

```
Cria pra mim uma skill chamada [nome-em-kebab-case].

O que ela faz:
1. [Gatilho] (ex: "toda sexta de manhã")
2. [Passo 1 — entrada] (ex: "lê conversas do Telegram dos últimos 7 dias")
3. [Passo 2 — processo] (ex: "agrupa dúvidas por categoria")
4. [Passo 3 — output] (ex: "salva em reports/[data].html")
5. [Passo 4 — entrega] (ex: "manda no Telegram tópico Operação")

Roda criar-skill e me mostra o SKILL.md gerado pra eu validar
antes de instalar.

Princípio A10: scope mínimo · só pede acesso ao que precisa.
```

### 3. Auditar skill antes de instalar

```
Quero instalar a skill [nome] de [github.com/X ou ClawHub/X].

Antes de aprovar, faz auditoria:

1. Lê o SKILL.md do repo · me resume em 3 linhas o que faz
2. Verifica os 4 critérios de skill confiável:
   - Última atualização <90 dias
   - README clara com exemplo
   - Autor responde issues
   - Compatível com OpenClaw atual
3. Lista quais permissões ela vai pedir
4. Diz se entra em conflito com skill já instalada

Reporta status: APROVAR / ATENÇÃO / REJEITAR.
Só instala depois que eu confirmar.
```

## Comandos `openclaw skills`

| Comando | Pra que serve |
|---------|---------------|
| `openclaw skills list` | Lista todas as skills instaladas |
| `openclaw skills install <name>` | Instala skill do ClawHub ou repo |
| `openclaw skills create` | Helper interativo pra criar skill |
| `openclaw skills test <name>` | Roda skill em modo teste |

## Onde achar mais skills (3 fontes oficiais)

| Fonte | O que tem |
|-------|-----------|
| **Anthropic Skills** ([github.com/anthropics/skills](https://github.com/anthropics/skills)) | Skills oficiais Anthropic (127k stars) |
| **awesome-openclaw** ([github.com/VoltAgent/awesome-openclaw-skills](https://github.com/VoltAgent/awesome-openclaw-skills)) | Awesome list curado pela comunidade |
| **ClawHub** ([clawhub.ai](https://clawhub.ai/)) | App store oficial OpenClaw |

**Critério pra adotar skill nova:** última atualização <90 dias · README clara · autor responde issues · funciona com OpenClaw atual.

## Princípios A10 aplicados a skills

1. **Scope mínimo por skill** — skill só pede acesso ao que precisa
2. **Audit em skills externas** — antes de instalar do ClawHub
3. **Revisão humana antes de instalar custom**
4. **Skill que toca segredo precisa rotação clara** — token no `.env`
5. **Skill em cron isolado por padrão** (`--session isolated`)

## Referências

- A8 (este cheatsheet complementa) · A7 (memória) · A9 (crons) · A10 (segurança)
- ClawHub: [clawhub.ai](https://clawhub.ai/)
- Doc OpenClaw skills: [docs.openclaw.ai/tools](https://docs.openclaw.ai/tools)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
