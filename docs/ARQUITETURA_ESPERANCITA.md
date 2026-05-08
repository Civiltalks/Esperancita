# Arquitetura da Esperancita - Etapa 1

Data: 2026-05-08

## Objetivo

Estruturar a Esperancita como agente OpenClaw com identidade, memoria, regras operacionais, skills, GitHub e caminho seguro para VPS.

## Base usada

Materiais lidos e consolidados:

- templates `IDENTITY`, `SOUL`, `USER`, `AGENTS`, `HEARTBEAT`;
- exemplo Amora;
- PRD de memoria;
- PRD de VPS Hostinger;
- skills existentes em `skills/starter`, `skills/operacional` e `skills/planejamento`;
- relatorios locais de instalacao;
- estado real de `C:\Users\aliss\.openclaw`.

## Estrutura criada

Arquivos raiz do workspace:

- `IDENTITY.md`
- `SOUL.md`
- `USER.md`
- `AGENTS.md`
- `TOOLS.md`
- `HEARTBEAT.md`
- `MAPA.md`
- `MEMORY.md`

Memoria:

- `memory/hot.md`
- `memory/context/decisions.md`
- `memory/context/lessons.md`
- `memory/context/people.md`
- `memory/context/business-context.md`
- `memory/context/security.md`
- `memory/context/integrations.md`
- `memory/context/pending.md`
- `memory/projects/esperancita-openclaw.md`
- `memory/projects/github-esperancita.md`
- `memory/projects/hostinger-vps.md`
- `memory/projects/transcricoes-whisper.md`
- `memory/sessions/2026-05-08.md`
- `memory/feedback/*.json`

Skills especificas:

- `skills/esperancita/status-operacional`
- `skills/esperancita/sincronizacao-github-segura`
- `skills/esperancita/preparar-deploy-hostinger`
- `skills/esperancita/governanca-memoria`
- `skills/esperancita/transcricao-whisper`

Etapa 2:

- `projects/esperancita-etapa2/PRD.md`

## Estado operacional

- OpenClaw local: funcional.
- GitHub: conectado e publicado.
- Telegram: configurado.
- OpenAI conversa: OAuth.
- API OpenAI: reservada para transcricao.
- Hostinger: API validada, SSH pendente.

## Validacoes executadas

- `openclaw config validate`: valido.
- `openclaw gateway status`: gateway local respondendo em `127.0.0.1:18789`.
- `openclaw skills check --agent main`: 77 skills totais, 33 elegiveis/visiveis; 5 skills novas da Esperancita prontas.
- `openclaw skills info status-operacional --agent main`: skill pronta e visivel.
- `openclaw skills info governanca-memoria --agent main`: skill pronta e visivel.
- `openclaw memory index --force`: 15/15 arquivos de memoria indexados, 16 chunks, dirty=no.
- Teste de agente local: resposta exata `ESPERANCITA_ARQUITETURA_OK` usando `provider=openai-codex`, `model=gpt-5.5`, `fallbackUsed=false`.

## Riscos controlados

- Segredos continuam fora do versionamento.
- Backups foram criados antes da estruturacao.
- `claudio` e `david` nao foram encontrados, mas foram registrados como agentes a preservar se aparecerem.
- `BOOTSTRAP.md` foi tornado referencia historica para nao reiniciar a identidade do agente.

## Pendencias

- Autorizar SSH na VPS Hostinger.
- Definir contexto humano/profissional detalhado.
- Definir crons reais e frequencia de proatividade.
- Executar Etapa 2 com arquivos definitivos de comportamento, atividades e criterios.
