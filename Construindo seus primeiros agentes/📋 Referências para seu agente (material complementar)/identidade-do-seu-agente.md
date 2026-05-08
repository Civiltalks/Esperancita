---
name: identidade-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A5]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra identidade do agente OpenClaw (A5). Cobre os 4 arquivos canônicos (SOUL · IDENTITY · AGENTS · USER) + USERS.md (corporativo) · diferença SOUL vs IDENTITY · anatomia detalhada de cada arquivo · 5 prompts prontos · comandos `openclaw context`.
---

# Identidade do seu agente — referência rápida (A5)

## A5 em 1 minuto (resumo executivo)

Identidade do agente = **5 arquivos** que respondem 5 perguntas distintas.

| Arquivo | Pergunta que responde | Quem atualiza | Frequência |
|---------|-----------------------|---------------|------------|
| **`SOUL.md`** | Quem ele É (personalidade · tom · valores) | Agente, em diálogo com aluno | Toda vez que tom não bate com o desejado |
| **`IDENTITY.md`** | O que ele FAZ (papel funcional · cargo) | Agente, em diálogo com aluno | Quando papel muda |
| **`AGENTS.md`** | Como ele se RELACIONA (organograma) | Agente · aluno revisa | Quando entra agente novo (A13) |
| **`USER.md`** | Quem é VOCÊ (perfil · família · negócios) | Agente captura · aluno valida | Toda mudança material no seu contexto |
| **`USERS.md`** (corporativo) | Quem são os USERS (plural — equipe) | Agente captura · admin valida | Quando entra/sai pessoa do time |

> **Frase-mãe da A5:** *"Identidade é a base. Contexto é o que dá vida. Quanto mais ele te conhece, mais ele orquestra."*

## SOUL.md vs IDENTITY.md — a confusão clássica

| Quesito | SOUL.md | IDENTITY.md |
|---------|---------|-------------|
| Pergunta | Quem ele É | O que ele FAZ |
| Conteúdo | Tom · personalidade · valores · jeito de responder | Cargo · responsabilidades · escopo |
| Exemplo Amora | "anti-hustle culture · direta sem hedge · vulnerável quando agrega" | "Chief of Staff do Bruno · opera Pixel + agentes + conteúdo" |
| Muda quando | Você não gosta do tom da resposta | Papel funcional muda |

**Teste rápido:** se você tá descrevendo *jeito de responder* → SOUL. Se você tá descrevendo *tarefa que ele faz* → IDENTITY.

## Anatomia do SOUL.md (5 seções típicas)

| Seção | Conteúdo | Exemplo |
|-------|----------|---------|
| **Tom** | Como ele fala | "Direto e conversacional · português BR sem formalismo" |
| **Comportamento default** | Padrões de resposta | "Opina forte · zero filler · sem emoji a menos que peça" |
| **Regras invariantes** | Always X / Never Y · linhas vermelhas | "Always solução simples primeiro" |
| **Pré-requisitos** | O que ele precisa antes de agir | "Sempre lê arquivo antes de editar" |
| **Anti-padrões** | O que NUNCA faz | "Nunca clichê de coaching · nunca formalidade corporativa" |

## Anatomia do USER.md (8 blocos)

| Bloco | Conteúdo | Por que importa |
|-------|----------|-----------------|
| **1. Perfil** | Nome + 2 linhas profissionais | Agente decide tom de resposta |
| **2. Negócios** | Quais são · qual é principal · qual gera caixa | Agente prioriza ação alinhada |
| **3. Família** | Esposa · filhos · contexto relevante | Agente respeita time-off |
| **4. Equipe** | Quem coordena com você · papéis · cadência | Agente sabe quem cobrar |
| **5. Tom preferido** | Direto · sem clichê · sem emoji · etc | Reforço do SOUL |
| **6. Restrições** | Coisas que NÃO faz por princípio | Agente para de propor isso |
| **7. Valores** | 3-5 frases-chave | Agente alinha decisões |
| **8. Contexto operacional** | Cidade · time zone · ferramentas | Agente respeita horário |

> **CRÍTICO (recap A10):** USER.md NÃO é cofre. Senha · token · API key vão pro `.env`. USER.md é perfil.

## 5 prompts prontos pra colar

### 1. Gerar SOUL.md inicial baseado em diálogo

```
Lê seu SOUL.md atual (deve estar raso, gerado pelo kit em A3).

Quero aprofundar sua personalidade. Vou descrever em linguagem natural
como quero que você responda — você captura em SOUL.md, mostra diff,
pede confirmação antes de salvar.

Tom: [direto / formal / técnico / casual / vulnerável / etc.]
Hedge: [opina forte / hedge frequente / só no que tem certeza]
Filler: [zero / aceita / específico]
Emoji: [zero / específico / livre]
Como discordar de mim: [pode discordar quando aumenta clareza /
                       sempre concorda / negocia]

Captura no SOUL e me mostra o resultado antes de salvar.
```

### 2. Estruturar USER.md em 8 blocos via diálogo

```
Lê seu USER.md atual.

Quero te ensinar quem eu sou de verdade. Vou te contar 8 blocos —
você captura em USER.md, organizado por seção, mostra diff, confirma.

1. Nome + 2 linhas de perfil profissional
2. Meus negócios (qual é principal · qual gera caixa · qual é estratégico)
3. Família (com contexto que afeta meu day a day)
4. Equipe (quem coordena comigo · papéis · cadência)
5. Tom que prefiro receber de você
6. Restrições (coisas que NÃO faço por princípio)
7. Valores (3-5 frases-chave)
8. Contexto operacional (cidade · time zone · ferramentas · cadência)

Princípio A10: NÃO coloca credencial em USER.md — só perfil.
```

### 3. Detectar inconsistência entre SOUL e USER (auditoria)

```
Faz auditoria de consistência entre SOUL.md e USER.md.

1. SOUL afirma X que NÃO está suportado por nada em USER?
2. USER afirma valor/restrição que NÃO se reflete em SOUL?
3. Tom do SOUL bate com tom desejado do USER?
4. Há regra que apareceu em SOUL mas devia estar em IDENTITY?

Me mostra inconsistências em formato de tabela.
NÃO altera nada sem confirmação.
```

## Comandos `openclaw context`

| Comando | Pra que serve |
|---------|---------------|
| `openclaw context show` | Mostra arquivos de contexto carregados no boot |
| `openclaw context reload` | Força reload do contexto após edição manual |
| `openclaw agent identity` | Lista agentes do workspace + identidade resumida |

## Referências

- A5 (este cheatsheet complementa) · A3 (Starter Kit) · A6 (workspace) · A7 (memória) · A10 (segurança)
- Doc OpenClaw `concepts/identity`: [docs.openclaw.ai/concepts/identity](https://docs.openclaw.ai/concepts/identity)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
