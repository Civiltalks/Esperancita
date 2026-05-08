---
name: workspace-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A6]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra workspace do agente OpenClaw (A6). Cobre estrutura canônica em 4 pastas raiz · MAPAs distribuídos (Princípio 12) · arquivos raiz · quando atualizar MAPA vs nunca · 5 prompts prontos.
---

# Workspace do seu agente — referência rápida (A6)

## A6 em 1 minuto (resumo executivo)

Workspace canônico = **4 pastas raiz** + **arquivos de identidade na raiz** + **MAPAs distribuídos** (1 por pasta).

| Pasta raiz | O que mora aqui | Quem mexe |
|------------|------------------|-----------|
| **`content/`** | Coisas que ele CRIA pra você (posts · drafts · materiais) | Agente cria · você revisa |
| **`memory/`** | Coisas pra LEMBRAR (decisões · pendências · context · dailies · projects) | Só o agente — território dele |
| **`skills/`** | Capacidades modulares (cobertura A8) | Agente curado · você cria custom |
| **`archive/`** | Coisas obsoletas/fechadas/encerradas (flat por mês) | Agente arquiva · você nunca deleta |

> **Frase-mãe da A6:** *"Workspace organizado = capacidade de escalar. Mapas em cada pasta = agente achando as coisas. Audit mensal = ele afiado pro próximo mês."*

## Árvore canônica (visual)

```
~/.openclaw/agents/<id>/
├── SOUL.md             ← persona (recap A5)
├── IDENTITY.md         ← papel funcional (recap A5)
├── AGENTS.md           ← organograma (recap A5 · cobertura A13)
├── USER.md             ← seu perfil (recap A5)
├── MEMORY.md           ← auto-conhecimento do agente (cobertura A7)
├── MAPA.md             ← lista as 4 pastas + onde encontrar cada coisa
├── HEARTBEAT.md        ← config de proatividade (cobertura A9)
├── content/            ← coisas que ele CRIA
│   └── MAPA.md         ← documenta a si mesma (Princípio 12)
├── memory/             ← coisas pra LEMBRAR
│   ├── MAPA.md
│   ├── hot.md          ← contexto quente (cobertura A7)
│   ├── 2026-05-02.md   ← daily SOLTA na raiz (padrão OpenClaw)
│   ├── context/        ← people, business, decisões, pendências
│   └── projects/       ← 1 arquivo por projeto + _index.md
├── skills/
│   └── MAPA.md
├── archive/
│   └── MAPA.md
└── .env                ← credenciais (NUNCA commita · cobertura A10)
```

## MAPAs distribuídos — Princípio 12

Cada pasta tem um `MAPA.md` local que documenta o que vive ali dentro.

### Por que NÃO um TOOLS.md monolítico

| Problema | Por quê |
|----------|---------|
| **Cresce sem controle** | Em 3 meses tem 800 linhas, ninguém atualiza, vira mentira oficial |
| **Lock-in cognitivo** | Agente carrega 800 linhas no contexto pra cada decisão |
| **Sem domínio** | Edição de um pedaço afeta tudo |

### O que MAPAs distribuídos resolvem

| Vantagem | Como |
|----------|------|
| **Cada parte sabe de si** | `memory/MAPA.md` documenta só `memory/` |
| **Carrega só o que precisa** | Agente vai salvar coisa em content? Lê só `content/MAPA.md` |
| **Manutenção localizada** | Atualização de uma pasta não afeta as outras |

## memory/ é território do agente

Princípio que pode ser contraintuitivo: aluno acha que *"é meu workspace, posso mexer em tudo"*. Pode — mas em `memory/` você atrapalha mais do que ajuda.

**Anti-padrão clássico:** Aluno cria `memory/notas-importantes/` aleatório. Resultado: vira lixeira que ninguém olha.

**Padrão correto:** Quando precisar de pasta nova, **conversa com o agente**. Ele decide onde encaixa baseado no MAPA.

## Archive — nunca deletar, sempre arquivar

```
archive/
├── 2026-04/
│   ├── projeto-X-encerrado.md
│   ├── decisao-revertida.md
│   └── pendencia-fechada-Y.md
├── 2026-05/
│   └── ...
└── MAPA.md
```

**Sem subpastas profundas. Sem taxonomia complexa.** Agente arquiva, fica lá, busca semântica acha quando precisa.

> **Histórico é vantagem competitiva.** Não joga fora — arquiva.

## 5 prompts prontos pra colar

### 1. Gerar MAPA.md raiz baseado em ls -R do workspace

```
Faz scan completo do workspace (ls -R em ~/.openclaw/agents/<id>/).

Lê o MAPA.md raiz atual e me responde:

1. As 4 pastas raiz esperadas existem (content, memory, skills, archive)?
2. Cada uma tem MAPA.md local?
3. MAPA raiz lista as 4 pastas + descreve onde guardar coisa nova?
4. Há pasta na raiz que NÃO está em nenhum MAPA (órfã)?
5. Há referência em MAPA pra pasta que NÃO existe (zumbi)?

Me devolve diagnóstico em tabela.
NÃO altera nada sem confirmação.
```

### 2. Auditar MAPAs órfãos e referências quebradas (audit mensal)

```
Roda audit do workspace. Olha:

1. Pendências em pendencias.md que tão fechadas — propõe arquivar
2. Projetos em projects/ que tão encerrados — propõe migrar pra archive
3. Daily notes na raiz de memory/ com mais de 14 dias — propõe arquivar
4. Pastas/arquivos que NÃO estão documentados em nenhum MAPA — lista
5. MAPAs que descreveram coisas que não existem mais — lista

Me devolve plano em lista. Eu aprovo em massa.
Princípio: archive em vez de delete. Sempre.
```

## Comandos `openclaw workspace`

| Comando | Pra que serve |
|---------|---------------|
| `openclaw workspace status` | Mostra estado do workspace |
| `openclaw workspace tree` | Árvore visual do workspace |
| `openclaw workspace cleanup` | Sugere limpeza (dry-run por default) |
| `openclaw workspace cleanup --apply` | Aplica limpeza após dry-run validado |

## Princípios de segurança aplicados (recap A10)

1. **Workspace isolado por agente** — cada agente paralelo tem `~/.openclaw/agents/<id>/` próprio
2. **`.env` NUNCA commita** — `.gitignore` default já protege
3. **Backup periódico em repo PRIVADO** — nunca público
4. **memory/ é território do agente** — você atrapalha se mexer manualmente
5. **Audit mensal de `.gitignore`**

## Referências

- A6 (este cheatsheet complementa) · A3 (Starter Kit) · A5 (identidade) · A7 (memória) · A8 (skills) · A10 (segurança) · A13 (multi-agente)
- Doc OpenClaw `concepts/workspace`: [docs.openclaw.ai/concepts/workspace](https://docs.openclaw.ai/concepts/workspace)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
