---
name: memoria-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A7]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra memória do agente OpenClaw (A7). Cobre os 3 tipos de memória (boot · sessão · semântica) · MEMORY.md · memory/hot.md · memory/YYYY-MM-DD.md · /new vs /compact · Memory Flush 70% · 5 prompts prontos.
---

# Memória do seu agente — referência rápida (A7)

## A7 em 1 minuto (resumo executivo)

Memória do agente = **3 tipos** trabalhando juntos + **3 arquivos canônicos** + **higiene de contexto**.

| Tipo | O que cobre | Quando ativa |
|------|-------------|--------------|
| **1. Padrão (boot)** | MEMORY.md + dailies 48h + MAPAs | Toda nova sessão · automático |
| **2. Sessão** | Chat atual no Telegram/Gateway | Enquanto você conversa · janela 200k tokens |
| **3. Semântica** | Busca por significado no workspace inteiro | Quando você pergunta · usa embeddings |

| Arquivo | Função | Quem mantém |
|---------|--------|-------------|
| **`MEMORY.md`** (raiz) | Auto-conhecimento estável (raramente muda) | Agente · auto-gerenciado |
| **`memory/hot.md`** | Contexto quente · estado do agora | Agente · auto-mantido (skill `/salve` empurra) |
| **`memory/YYYY-MM-DD.md`** | Dailies (sessões diárias · padrão OpenClaw) | Agente · purga após 14 dias |

> **Frase-mãe da A7:** *"Memória sem higiene = agente lerdo. Higiene sem memória = começar do zero todo dia. Os dois juntos = ele escala com você."*

## Os 3 tipos de memória — anatomia

### 1. Memória padrão (boot) — como ele acorda

| O que faz | Detalhe |
|-----------|---------|
| Lê `MEMORY.md` | Long-term self-knowledge |
| Lê `memory/hot.md` | Contexto quente · top prioridades · prazos críticos |
| Lê dailies de hoje + ontem | 48h de contexto (padrão OpenClaw) |
| Lê SOUL/IDENTITY/USER/AGENTS | Identidade (recap A5) |
| Carrega MAPAs do workspace | Sabe onde tá cada tipo de coisa (recap A6) |

### 2. Memória de sessão — chat atual

Janela de contexto da conversa em curso. Tem limite — **200k tokens com GPT-5.5**.

**Sintomas de saturação:**
- Agente lento (demora pra responder)
- Não responde (trava no meio)
- Alucina (inventa contexto · mistura conversas)
- Perde contexto antigo

### 3. Memória semântica — busca por significado

Sistema mais poderoso. Auto-ativada com OpenAI API key da A1.

**Como funciona (alto nível):**
1. Agente roda embeddings de cada arquivo do workspace · guarda vetores
2. Você pergunta com significado · agente vetoriza pergunta
3. Retorna arquivos com vetores próximos · sintetiza resposta

## /new vs /compact — quando usar cada

| Comando | Quando usar | O que faz |
|---------|-------------|-----------|
| **`/new`** | Mudou de assunto · sessão saturada | Limpa contexto inteiro · começa zero |
| **`/compact`** | Sessão grande mas conversa ainda relevante | Comprime histórico mantendo essência |
| **`/compact Focus on [tema]`** | Compacta com foco em tema específico | Mantém foco · descarta resto |
| **`/status`** | Diagnóstico · sentir lentidão | Mostra uso de contexto · sessão atual · modelo |

> **Princípio absoluto (recap A0):** *"Salve antes de limpar."* Memory Flush automático ajuda mas não é 100% (~70% de confiabilidade real).

## Memory Flush — feature nativa

Antes da compactação automática disparar, agente faz um **"silent memory flush"** — tenta salvar nas pastas certas antes de comprimir.

**Confiabilidade real (estimativa Bruno):** ~**70%** das vezes funciona limpo.

**Implicação:** você ajuda salvando manual quando o assunto importa. Não confia 100% no flush automático.

## 5 prompts prontos pra colar

### 1. Atualizar MEMORY.md com auto-conhecimento

```
Lê seu MEMORY.md atual.

Nas últimas [X dias / Y sessões] eu te corrigi sobre [tema/padrão]:
- [Correção 1: ex "use prosa, não bullets desnecessários"]
- [Correção 2: ex "número específico, não arredondado"]
- [Correção 3: ex "sem emoji a menos que eu peça"]

Promove os aprendizados DURÁVEIS pra MEMORY.md (não conjunturais).
Mantém hot.md com o que ainda é contexto quente da semana.

Mostra diff antes de salvar. NÃO mexe em SOUL.md.
```

### 2. Investigar "por que ele esqueceu de X?" (debug de memória)

```
Investiga por que você esqueceu de [DECISÃO / CONTEXTO específico].

Diagnóstico em ordem:

1. Roda busca semântica: openclaw memory search "[query do tema]"
2. Lê hot.md atual: tema aparece? Se não, por que saiu?
3. Lê MEMORY.md: tema deveria estar aqui (durável) e não tá?
4. Olha dailies dos últimos 14 dias
5. Olha archive/

Me devolve diagnóstico em tabela.
Propõe ação corretiva (reindex · refazer hot · salvar manual).
```

### 3. Reindexar memória semântica após mudança grande

```
Acabei de [MUDANÇA: ex "mover 50 arquivos", "reorganizar pasta X"].

Memória semântica precisa reindexar pra refletir nova estrutura.
Roda em ordem:

1. openclaw memory status
2. openclaw memory index --force
3. Valida: openclaw memory search "[query teste]"
4. Atualiza MAPAs afetados pela mudança

Me reporta antes/depois do índice.
```

## Comandos `openclaw memory` e `openclaw sessions`

### Memória semântica

| Comando | Pra que serve |
|---------|---------------|
| `openclaw memory status` | Estado do índice · # de arquivos · última atualização |
| `openclaw memory search "<query>"` | Busca semântica · retorna arquivos ranqueados |
| `openclaw memory index --force` | Reindexar workspace inteiro |

### Higiene de sessão (no chat)

| Comando | Pra que serve |
|---------|---------------|
| `/new` | Nova sessão limpa |
| `/new <model>` | Nova sessão trocando modelo |
| `/compact` | Compacta contexto mantendo essência |
| `/status` | Mostra uso de contexto · sessão atual · modelo ativo |

## Princípios de segurança aplicados (recap A10)

1. **Memória NÃO é log de chat** — credencial NÃO vai pra memória
2. **Sessões antigas auto-purgam** — após 14 dias dailies vão pra archive/
3. **Workspace isolado em Docker**
4. **`.env` nunca em memória**
5. **Memória semântica é local** (vetores ficam no workspace)

## Referências

- A7 (este cheatsheet complementa) · A1 (setup) · A3 (Starter Kit) · A5 (identidade) · A6 (workspace) · A9 (crons) · A10 (segurança)
- Doc OpenClaw `concepts/memory`: [docs.openclaw.ai/concepts/memory](https://docs.openclaw.ai/concepts/memory)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
