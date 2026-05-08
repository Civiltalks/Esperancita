---
name: governanca-memoria
status: ATIVO
category: esperancita
owner: aluno
version: 1.0
mode: guided
estimated_time: 3-15min
model_compatible: [gpt-5, gpt-5.5]
description: Use quando o usuario pedir para lembrar, organizar memoria, registrar decisoes, preparar comportamento ou consolidar sessao. Atualiza MEMORY.md e topic files sem salvar segredos.
---

# Governanca de Memoria

## Promessa

Transformar informacao solta em memoria persistente, organizada e segura.

## Onde salvar

- Decisao permanente: `memory/context/decisions.md`
- Erro/aprendizado: `memory/context/lessons.md`
- Pessoa/contato: `memory/context/people.md`
- Projeto: `memory/projects/{nome}.md`
- Pendencia: `memory/context/pending.md`
- Dia atual: `memory/sessions/YYYY-MM-DD.md`
- Prioridade imediata: `memory/hot.md`

## Regras

- Nao salvar token real.
- Nao salvar segredo completo.
- Nao duplicar arquivos grandes em `MEMORY.md`.
- Se o usuario disser "lembra disso", escolher topic file correto.
- Se for comportamento do agente, atualizar tambem `SOUL.md` ou `AGENTS.md` quando fizer sentido.

## Fechamento de sessao

Antes de encerrar trabalho relevante:

1. Registrar o que foi feito.
2. Registrar decisoes.
3. Registrar pendencias.
4. Registrar licoes.
5. Atualizar projeto ativo.
