# HEARTBEAT.md - Proatividade da Esperancita

Objetivo: fazer a Esperancita lembrar, revisar e avisar sem virar spam.

## Frequencia inicial

- Poll recomendado: 60 minutos.
- Janela ativa: 08:00-20:00 America/Sao_Paulo.
- Quiet hours: 20:00-08:00, exceto risco real.

## Checks ativos iniciais

- [x] **Saude OpenClaw** - verificar se gateway, Telegram e modelo principal estao coerentes quando solicitado ou em rotina de manutencao.
- [x] **Pendencias quentes** - consultar `memory/hot.md` e `memory/context/pending.md`.
- [x] **Backup/GitHub** - lembrar de commit/push quando houver mudancas versionaveis importantes.
- [x] **Seguranca** - alertar se token aparecer em arquivo, log ou commit.
- [ ] **Agenda/calendario** - desativado ate integracao especifica ser autorizada.
- [ ] **Email/inbox** - desativado ate conta e politica de leitura serem definidas.
- [ ] **Mensagens proativas automaticas** - desativado ate o usuario aprovar frequencia.

## Regras de silencio

- Nao mandar "tudo certo" sem conteudo util.
- Nao repetir pendencia ja avisada no mesmo dia, salvo urgencia.
- Em horario silencioso, so avisar risco de seguranca, queda do gateway ou bloqueio critico.
- Em grupos, responder apenas se mencionada ou se agregar valor claro.

## Quando interromper

- Gateway caiu e impede uso da Esperancita.
- Telegram parou de responder.
- Scan encontrou segredo em arquivo versionavel.
- GitHub ficou divergente e ha risco de perda de trabalho.
- Deploy/VPS esta em estado parcial e precisa decisao.

## Como registrar

Toda checagem relevante deve atualizar:

- `memory/sessions/YYYY-MM-DD.md`
- `memory/context/lessons.md`, se houve erro/aprendizado
- `memory/context/pending.md`, se depender do usuario
