---
name: crons-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A9]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra crons + heartbeat do agente OpenClaw (A9). Cobre cron vs heartbeat · 4 categorias com 10+ exemplos · Revisão do Dia · meta-cron de auditoria · 7 ideias de heartbeat · 5 prompts prontos.
---

# Crons do seu agente — referência rápida (A9)

## A9 em 1 minuto (resumo executivo)

OpenClaw tem **2 mecanismos de proatividade complementares**:

- **Cron** — timing exato (segunda 9h sharp), tarefa isolada, output entregue direto no canal. *"O que TEM que acontecer."*
- **Heartbeat** — drift de timing OK (~30min de janela), múltiplas checks pequenas em batch, agente decide se age ou fica quieto. *"O que PODE valer a pena."*

**Frase-mãe da A9:** *"cron = onde você dá super poderes ao agente. Sem cron, ele é assistente. Com cron, ele é operação."*

Você sai da A9 com **3 crons suficientes pra começar:** Revisão do Dia (18h) + meta-cron de auditoria (7h) + 1 cron próprio do seu workflow.

## Cron vs heartbeat — quando usar cada um

| Dimensão | **Heartbeat** | **Cron** |
|----------|--------------|----------|
| **Timing** | Drift OK (~30min de janela) | Exato ("segunda 9h sharp") |
| **Tarefa** | Múltiplas checks pequenas em batch | 1 task isolada |
| **Contexto** | Usa histórico recente + lê `memory/hot.md` | Sessão isolada (default) |
| **Custo API** | Reduz chamadas (1 turno = N checks) | 1 chamada por trigger |
| **Output** | Conversa contigo (ou silêncio) | Entrega direto no canal |

## 4 categorias de cron — 10+ exemplos

### 1. Monitoramento (saúde do sistema)
- **Health check semanal** · valida que API key, OAuth, canais e crons tão OK
- **Auditar workspace mensal** · checa MAPAs, MEMORY, skills
- **Auditar os próprios crons** (meta-cron) · cron que checa se os outros rodaram OK

### 2. Pesquisa & estudo
- **Pesquisas de conteúdo** · tendências do dia no seu nicho
- **Ler documentação nova** de ferramenta que você usa
- **Analisar próprias memórias** pra aprender padrões sobre você (recap A7)

### 3. Sumarização & relatórios
- **Relatório semanal** (vendas · KPIs · métricas)
- **Tickets de suporte** · agente lê, classifica por categoria + urgência
- **Newsletter da comunidade**

### 4. Planejamento & reflexão
- **Revisão do Dia** (cron-âncora 18h) · agente fecha o dia e prepara o seguinte
- **Auditar notas das pessoas** pra ver o que aprenderam

> **Princípio:** se cron novo não couber em nenhuma das 4 categorias, provavelmente não é cron — é skill que você roda manualmente.

## 4 comandos naturais cobrem 100% do uso

| Intenção | Prompt natural |
|----------|----------------|
| Criar cron | `cria um cron toda manhã 8h que olha minhas pendências e me manda priorizadas` |
| Listar crons | `me lista os crons que eu tenho` |
| Apagar cron | `apaga o cron das pendências` |
| Rodar agora (teste) | `roda o cron de revisão do dia agora` |

## Revisão do Dia (cron-âncora 18h)

**Você chega de manhã e o agente já preparou amanhã pra você.**

### Prompt pra criar Revisão do Dia

```
cria um cron toda dia 18h chamado revisao-do-dia que:

1. Lê minha daily note do dia (memory/YYYY-MM-DD.md) e cruza
   com memória semântica
2. Lista o que ficou pendente (cruza decisões do dia com
   pendencias.md)
3. Alerta sobre amanhã: lê calls, deadlines, prazos do dia
   seguinte
4. Manda resumo no Telegram tópico Operação no formato:
   - Hoje fiz: ...
   - Aberto: ...
   - Amanhã: ...
5. Roda em sessão isolada (não polui contexto da sessão atual)
```

## Meta-cron de auditoria (cron que audita os próprios crons)

Funcionário precisa de supervisor — mesmo se o supervisor for ele mesmo.

```
cria um cron toda manhã 7h que checa todos os crons que
rodaram nas últimas 24h, lista os que deram OK e os que
falharam, e me manda resumo no Telegram tópico Operação.

Se algum falhou, inclui o erro pra eu poder corrigir.
Roda em sessão isolada e usa --light-context.
```

> **Frase-mãe:** *você não confia 100% em cron. Mas você confia em cron que audita cron.*

## Heartbeat — o agente que respira

A cada N minutos o agente recebe uma "batida" — uma mensagem do tipo "tô vivo, alguma coisa nova?".

### Os 2 arquivos que fazem heartbeat funcionar

| Arquivo | Função | Quem mantém |
|---------|--------|-------------|
| `HEARTBEAT.md` | **COMO ele vigia** — frequência do poll, checks, regras de silêncio | Aluno (raro) |
| `memory/hot.md` | **O QUE ele vigia** — prioridades, prazos, decisões | Agente (auto) |

### 7 ideias de heartbeat pra experimentar

- **Inbox triage** — emails não-lidos das últimas 4h, classifica em urgente/pode esperar/lixo
- **Calendário próximo** — checa próximas 24-48h, lembra do que tem amanhã
- **Mention sweep** — checa LinkedIn/Twitter, manda só relevantes
- **Pendências paradas** — itens com nome de terceiro parado há 3+ dias
- **Memory maintenance** — extrai aprendizados duráveis pra MEMORY.md
- **Weather guard** — se tiver evento externo hoje, checa previsão
- **News watch** — checa 2-3 fontes que importam pro seu negócio

### Regras de silêncio (anti-spam)

- **Quiet hours 23h–8h** — só interrompe se for urgência real
- **Já checou nos últimos 30min?** — não checa de novo
- **Nada novo?** — silêncio (não manda "tudo certo!" gratuito)
- **Reach out só quando:** email importante chegou · evento <2h · achou algo interessante

## Comandos `openclaw cron`

| Comando | Pra que serve |
|---------|---------------|
| `openclaw cron add` | Adiciona cron novo |
| `openclaw cron list` | Lista todos os crons configurados |
| `openclaw cron run --id <id>` | Executa cron agora (sem esperar horário) |
| `openclaw cron runs --id <id>` | Histórico de execuções |
| `openclaw cron edit --id <id>` | Edita prompt, horário ou flags |
| `openclaw cron rm --id <id>` | Remove cron |
| `openclaw cron enable / disable` | Pausa ou retoma cron sem deletar |

### Flags úteis

| Flag | Pra que serve |
|------|---------------|
| `--session isolated` | Cron roda em sessão limpa (default) |
| `--light-context` | Carrega só o essencial (mais rápido, custo menor) |
| `--no-deliver` | Executa mas não envia output (útil pra teste) |
| `--at <datetime>` | Cron de execução única |

## Princípios A10 aplicados a crons + heartbeat

1. **Cap mensal por cron** — 3 crons úteis > 15 crons enroscados
2. **Audit log de cada execução** — `openclaw cron runs --id <id>`
3. **Heartbeat com regras de silêncio** — anti-spam
4. **Sessão isolada por padrão** — `--session isolated`
5. **Meta-cron audita os crons**
6. **Skill em cron precisa carregar tudo explicitamente**

## Referências

- A9 do roteiro principal · A2 (cockpit) · A7 (memória) · A8 (skills) · A10 (segurança) · A12 (integrações)
- Doc OpenClaw cron: [docs.openclaw.ai/cli/cron](https://docs.openclaw.ai/cli/cron)

---

> **Anti-hype:** não cria 15 crons no day 1. Maioria fica órfã. **3 crons úteis > 15 crons enroscados.** Vai adicionando conforme aparecer repetição real.

📌 Atualizado em 04/05/2026 · Pixel Educação
