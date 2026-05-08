---
name: transcricao-whisper
status: ATIVO
category: esperancita
owner: aluno
version: 1.0
mode: guarded
estimated_time: variavel
model_compatible: [gpt-5, gpt-5.5]
description: Use quando o usuario enviar audio, pedir transcricao, resumo de audio, ou validar Whisper. Mantem API OpenAI restrita a transcricao e nao troca o modelo principal da Esperancita.
---

# Transcricao Whisper

## Politica

Conversas da Esperancita usam OAuth/conta OpenAI. A API OpenAI e permitida apenas para:

- transcricao;
- Whisper;
- embeddings/memoria semantica quando necessario;
- chamadas API diretas explicitamente solicitadas.

## Validacao

Antes de pedir chave ao usuario, detectar:

```powershell
[Environment]::GetEnvironmentVariable('OPENAI_API_KEY','User') -ne $null
[Environment]::GetEnvironmentVariable('OPENAI_API_KEY','Process') -ne $null
```

Se existir, validar sem imprimir a chave.

## Regras

- Nunca registrar a chave.
- Nunca colar chave em arquivo versionado.
- Nunca alterar modelo principal para `openai/gpt-*` via API.
- Se transcricao falhar, registrar erro e manter conversa via OAuth.

## Saida

Ao transcrever:

- transcricao fiel;
- resumo, se pedido;
- acoes extraidas, se pedido;
- local onde a transcricao foi salva, se for salva.
