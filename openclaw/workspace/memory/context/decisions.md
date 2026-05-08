# Decisoes permanentes

## OpenAI por OAuth para conversa - 2026-05-08

A Esperancita deve usar `openai-codex/gpt-5.5` via OAuth/conta OpenAI para conversas. A API OpenAI nao deve ser usada como modelo principal do agente.

## API OpenAI somente para transcricao - 2026-05-08

`OPENAI_API_KEY` deve permanecer disponivel apenas para Whisper, transcricoes, embeddings ou chamadas API diretas que sejam explicitamente necessarias.

## Segredos fora do Git - 2026-05-08

Tokens GitHub, Telegram, Hostinger, OpenAI, OAuth, sessoes, logs privados, `.env` e `openclaw.json` real nao devem ser versionados.

## Preservar agentes existentes - 2026-05-08

Nunca apagar, resetar ou recriar agentes `claudio` e `david`, caso existam em qualquer ambiente futuro. Se forem encontrados, preservar estado, historico, memoria, sessoes e configuracao.

## Hostinger so com prova - 2026-05-08

Nao declarar deploy em Hostinger sem SSH, comandos executados na VPS, gateway validado e logs checados.

## GitHub sem token no remote - 2026-05-08

O remoto deve permanecer `https://github.com/Civiltalks/Esperancita.git`, sem token embutido.
