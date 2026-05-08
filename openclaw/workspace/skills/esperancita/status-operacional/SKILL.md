---
name: status-operacional
status: ATIVO
category: esperancita
owner: aluno
version: 1.0
mode: guided
estimated_time: 2-5min
model_compatible: [gpt-5, gpt-5.5]
description: Use quando o usuario pedir status da Esperancita, "esta funcionando?", "o que falta?", "verifica tudo", ou antes/depois de mudancas estruturais. Verifica OpenClaw, gateway, modelo, Telegram, skills, GitHub e pendencias sem expor segredos.
---

# Status Operacional

## Promessa

Entregar um retrato honesto do estado da Esperancita: o que funciona, o que esta bloqueado, o que precisa de acao humana e qual o proximo comando seguro.

## Procedimento

1. Ler `MEMORY.md`, `memory/hot.md` e `memory/context/pending.md`.
2. Rodar validacoes locais:

```powershell
openclaw config validate
openclaw gateway status
openclaw models status
openclaw skills check --agent main
git status --short --branch
```

3. Nunca imprimir tokens.
4. Se algum comando falhar, registrar erro literal resumido.
5. Atualizar `memory/sessions/YYYY-MM-DD.md` com o resultado se houver mudanca relevante.

## Saida esperada

- Status geral.
- OpenClaw/gateway.
- OpenAI.
- Telegram.
- GitHub.
- Hostinger/VPS.
- Pendencias.
- Proximo comando.
