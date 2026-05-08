---
name: multi-agente
status: ATIVO
category: cheatsheet
referenced_by: [A13]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra decisão de multi-agente — quando vale, 2 caminhos (subagente vs paralelo), arquitetura por plataforma, comunicação real entre agentes (4 caminhos), AGENTS.md como organograma.
---

# Multi-agente — referência rápida (A13)

## Pergunta zero: 1 agente ou vários?

**Resposta honesta**: maioria absoluta dos PME, **1 agente bem configurado resolve**. Multi-agente é refinamento.

### 4 sinais que VALE evoluir

1. Agente único tá lento (context rot · threads pesadas)
2. Você fala 2 línguas operacionais distintas (ex: marketing + dev) e ele confunde
3. Você tem time/funcionários e quer dar agente próprio pra cada
4. Você quer delegação 24/7 (1 vigia inbox enquanto outro escreve)

### Custo REAL de cada agente extra

> **3 agentes ≠ 3x trabalho. Mais perto de 5x.** Multiplicar agentes multiplica manutenção (SOULs · USERs · credenciais · monitoramento · skills · comunicação).

### Sintomas de overengineering (revisar)

| Sintoma | Diagnóstico |
|---------|-------------|
| "Vou criar 5 agentes só porque é legal" | Estética > função. Volta pra 1 |
| Cada agente fica ocioso 90% do dia | Sub-utilização — junte funções |
| Custo dobrou e produtividade não | ROI ruim — reverta |
| Você passa mais tempo orquestrando que produzindo | Overhead > benefício |

## Os 2 caminhos quando vale evoluir

| Aspecto | **Subagente** (`/subagents spawn`) | **Agente paralelo** (entidade separada) |
|---------|---------------------|-------------------------------|
| O que é | Background run · async · resultado anunciado quando termina | Entidade separada · SOUL/IDENTITY/USER próprios |
| Custo de **criar** | Baixo — comando direto | Alto |
| Custo de **manter** | Quase zero | 5x trabalho |
| Identidade | **Limitada** — só herda `AGENTS.md` + `TOOLS.md` | Completa — SOUL/IDENTITY/USER próprios |
| Memória | **Sandbox isolado** por execução | Memória própria contínua (MEMORY.md) |
| Aparece no seu Telegram? | Não — invisível | Sim — handle próprio |
| Ideal pra | Tarefas pontuais (pesquisa, análise PDF) | Domínios contínuos (atendimento, conteúdo) |

**Princípio**: *"Subagente é **execução background**. Agente paralelo é **entidade separada**."*

### Decisão prática

- Tarefa pontual? → **Subagente** (sempre que dúvida, comece por aqui)
- Domínio contínuo + 4 sinais acima? → **Agente paralelo**

## Arquitetura por plataforma

| Plataforma | Limite | Como funciona |
|------------|--------|---------------|
| **Managed (curso default)** | **1 OpenClaw por plano** | Múltiplos agentes coexistem **dentro do mesmo workspace** |
| **VPS standalone (bônus R1-R4)** | Até **3 OpenClaws na mesma VPS** | Cada OpenClaw é independente · containers Docker separados |

## Como agentes conversam entre si — 4 caminhos REAIS

> **NÃO existe DM interna direta entre agentes em runtime** — comunicação acontece via mecanismos abaixo.

| Caminho | Mecanismo real | Quando usar |
|---------|---------------|-------------|
| **Subagente via spawn** | `/subagents spawn <agentId> "<task>"` · async | Delegar tarefa específica |
| **Mention em canal compartilhado** | `@amora @openclawzinho ...` · `requireMention: true` | Aluno orquestra explícito |
| **Arquivo compartilhado** | Agente A escreve em `~/.openclaw/shared/notes/` · Agente B lê | Dump de contexto pesado |
| **Trigger via cron + `openclaw agent --agent <id>`** | Cron de B detecta evento de A · roda comando programático | Automação async |

**Princípio**: *"Por default, agentes não se veem em runtime. **Você decide** quando e como cooperam."*

## Comandos `/subagents`

```
/subagents spawn <agentId> "<task>" [--model <model>] [--thinking <level>]
```

### Modos de contexto

- **`isolated` (default)** — sandbox limpo, sem acesso à transcrição do agente pai. Token-economy.
- **`fork`** — herda contexto pai. Use só quando subagente precisa de histórico.

### Limitação importante

> Sub-agent context só injeta `AGENTS.md` + `TOOLS.md` (não SOUL.md, IDENTITY.md, USER.md).

Sub-agent é **sandbox isolado com função específica**, não clone total. Pra ter identidade própria persistente → **agente paralelo**.

## AGENTS.md como organograma

### O que tem em AGENTS.md

| Seção | Conteúdo |
|-------|----------|
| **Quem é cada agente** | Handle · papel · modelo · escopo |
| **Quem chama quem** | Subagentes disponíveis · agentes paralelos com handoff |
| **Onde cada um vive** | Workspace · canais · integrações |
| **Permissões cruzadas** | Cada um tem scope próprio (recap A10) |
| **Governance** | Cap de custo mensal por agente · audit log |

## 4 prompts prontos pra colar

### 1. Análise honesta — preciso evoluir pra multi-agente?

```
Quero analisar honestamente se faz sentido evoluir pra multi-agente
agora. Vai na doc oficial em https://docs.openclaw.ai/concepts/multi-agent
e me responde:

1. Quais dos 4 sinais de "vale evoluir" se aplicam ao meu uso atual?
2. Tô em risco de cair em algum dos 6 sintomas de overengineering?
3. Se faço sentido, qual caminho recomenda PRIMEIRO — subagente
   pontual OU agente paralelo?
4. Custo estimado de manutenção mensal (multiplicador 5x sobre o que
   tenho hoje)?

Se a resposta for "ainda não vale", me diz claramente. Não invente
problema pra justificar evolução.
```

### 2. Criar subagente especialista

```
Quero criar um subagente especialista pra tarefas pontuais de
[pesquisa profunda / análise de documento / geração de imagem].

Vai na doc oficial em https://docs.openclaw.ai/tools/subagents,
lê como criar, me explica:

1. Como configurar o agentId (registrar em AGENTS.md)
2. Quais TOOLS.md ele precisa (scope mínimo)
3. Modelo recomendado (Haiku pra task barata)
4. Modo de contexto: isolated (default) vs fork

Configura tudo, registra em AGENTS.md, me dá comando exato pra
testar com 1 task simples primeiro.
```

### 3. Criar agente paralelo dedicado a 1 canal Telegram

```
Quero criar um SEGUNDO agente paralelo dedicado APENAS ao canal
Telegram [DESCREVE O CANAL].

NÃO quero que ele acesse outros canais da Amora. NÃO quero que ele
veja contexto pessoal meu. Quero workspace, identidade e memória
SEPARADOS.

Executa em ordem:

1. Bot novo no @BotFather (NÃO reusar o token da Amora)
2. Workspace isolado em ~/.openclaw/agents/<nome>/ com SOUL/IDENTITY/MEMORY
3. Conectar SÓ a este canal (escopo restrito ao chat_id)
4. Registra em AGENTS.md
5. Validação: manda mensagem no canal pra confirmar

Princípios A10:
- Scope mínimo (token só pra ESTE bot)
- Identidade própria (SOUL/IDENTITY/MEMORY isolados)
- Cap mensal de custo
- Audit log de mensagens primeiros 30 dias
```

## Princípios de segurança aplicados (recap A10)

1. **Cada agente com scope próprio** — não compartilhe credenciais
2. **AGENTS.md vivo e auditado**
3. **Cap de custo por agente**
4. **Monitoramento diário primeiros 30 dias**
5. **`requireMention: true` em canais compartilhados**
6. **Defesa anti-prompt-injection no SOUL** de cada agente paralelo

## Troubleshooting comum

| Sintoma | Causa provável | Ação |
|---------|----------------|------|
| `/subagents spawn` retorna "agentId not found" | Subagente não registrado em AGENTS.md | Adiciona seção do subagente |
| 2 agentes respondendo no mesmo canal | `requireMention: false` ou config incorreta | Configurar `requireMention: true` em ambos |
| Loop infinito Amora ↔ openclawzinho | Ambos com handoff sem condição de parada | Adicionar "max 1 handoff por thread" no AGENTS.md |
| Custo dobrou em 1 mês | Cron de subagente disparando demais | `openclaw cron list` · validar frequência |

## Referências

- A13 · A5 (AGENTS.md) · A9 (cron) · A10 (segurança operacional)
- Doc OpenClaw multi-agent: [docs.openclaw.ai/concepts/multi-agent](https://docs.openclaw.ai/concepts/multi-agent)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
