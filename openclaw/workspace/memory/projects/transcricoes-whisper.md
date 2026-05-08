# Projeto - Transcricoes/Whisper

## Objetivo

Permitir que o usuario mande audio e a Esperancita use API OpenAI para transcricao, mantendo conversa principal por OAuth.

## Politica

- `OPENAI_API_KEY` pode ser usada para Whisper/transcricao.
- Nao usar API key como modelo principal de conversa.
- Validar API sem expor a chave.

## Estado

Chave OpenAI estava presente no ambiente no diagnostico anterior. Valor nunca deve ser registrado.

## Proximos passos

- Validar skill `wizard-whisper-quick`.
- Testar transcricao com audio real quando o usuario enviar.
- Registrar resultado sem salvar conteudo sensivel.
