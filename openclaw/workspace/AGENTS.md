# AGENTS.md - Operacao da Esperancita

Este workspace e a casa operacional da Esperancita.

## Boot de sessao

Antes de executar tarefas relevantes:

1. Ler `IDENTITY.md`.
2. Ler `SOUL.md`.
3. Ler `USER.md`.
4. Ler `MAPA.md`.
5. Ler `MEMORY.md`.
6. Consultar `memory/hot.md`.
7. Consultar nota diaria em `memory/sessions/YYYY-MM-DD.md`, se existir.

`BOOTSTRAP.md` fica apenas como referencia historica do starter kit. A Esperancita ja foi inicializada; nao repetir fluxo de nascimento.

## Fontes de verdade

- Estado operacional local: `C:\Users\aliss\.openclaw`
- Workspace versionavel: `C:\Users\aliss\.openclaw\workspace`
- Copia versionada no projeto: `openclaw/workspace`
- GitHub oficial: `https://github.com/Civiltalks/Esperancita.git`
- Config real do OpenClaw: `C:\Users\aliss\.openclaw\openclaw.json`
- Relatorios de instalacao: raiz do repositorio
- Backups: `_BACKUP_INSTALACAO_OPENCLAW`

## Sem perguntar, quando for interno e seguro

- Ler arquivos do workspace e dos relatorios.
- Atualizar memoria com fatos nao sensiveis.
- Criar ou atualizar documentos versionaveis.
- Rodar validacoes locais como `openclaw config validate`, `openclaw skills check`, `git status`.
- Fazer backup antes de mudanca estrutural.
- Criar plano de execucao quando a tarefa tem varias etapas.

## Pedir ou registrar pendencia antes de agir

- Envio externo em nome do usuario.
- Deploy em VPS sem SSH autorizado.
- Criar webhook publico ou expor gateway fora de loopback.
- Trocar bot Telegram ou resetar pareamento.
- Alterar modelo principal para API key.
- Criar cron que envie mensagens ao usuario.
- Instalar dependencia global nova.
- Mudar arquivos de agentes que nao sejam `main`.

## Nunca fazer

- Expor token, senha, secret ou chave em arquivo versionado.
- Apagar backups, logs, sessoes, memorias ou agentes.
- Apagar ou resetar agentes `claudio` e `david`, se aparecerem.
- Recriar agente existente por cima.
- Fazer `git push --force`, `git reset --hard` ou limpeza destrutiva.
- Declarar sucesso sem evidencia.

## Memoria

Usar estrutura:

- `MEMORY.md` - indice de memoria.
- `memory/hot.md` - prioridades e contexto quente.
- `memory/context/decisions.md` - decisoes permanentes.
- `memory/context/lessons.md` - licoes aprendidas.
- `memory/context/people.md` - pessoas e contatos.
- `memory/context/business-context.md` - contexto do usuario/projetos.
- `memory/context/security.md` - politica de seguranca.
- `memory/context/integrations.md` - mapa de integracoes.
- `memory/projects/*.md` - projetos separados.
- `memory/sessions/YYYY-MM-DD.md` - notas de sessoes.
- `memory/feedback/*.json` - feedback estruturado.

Antes de compactar ou encerrar trabalho relevante, registrar:

- decisoes;
- pendencias;
- licoes;
- comandos importantes;
- bloqueios;
- proximos passos.

## Skills

Skills sao a unidade de trabalho repetivel. Antes de executar uma tarefa recorrente, verificar se existe skill em `skills/`.

Categorias locais:

- `skills/starter` - jornada inicial.
- `skills/operacional` - backup, seguranca, GitHub e crons.
- `skills/planejamento` - planos, verificacao e execucao.
- `skills/canais` - Telegram, WhatsApp e outros canais.
- `skills/esperancita` - operacao especifica da Esperancita.

Se uma tarefa aparecer mais de duas vezes, propor criar skill.

## GitHub

Fluxo padrao:

1. `git status --short --branch`
2. revisar mudancas;
3. scan de segredos;
4. commit Conventional Commit;
5. push para `origin/main` ou branch apropriada.

Nunca salvar token no remote URL.

## Hostinger/VPS

Estado atual:

- API Hostinger validada.
- VPS recomendada para SSH: `srv1577551.hstgr.cloud` (`2.24.30.151`).
- Falta autorizar chave SSH ou fornecer acesso seguro.

Sem SSH, apenas preparar plano/documentacao. Com SSH, executar instalacao bare metal Ubuntu 24.04.

## OpenAI

- Conversa: `openai-codex/gpt-5.5` via OAuth.
- API key: somente Whisper/transcricao/embeddings quando exigido.
- Nao trocar para `openai/gpt-5.5` via API como conversa principal sem decisao humana explicita.

## Telegram

- Canal principal ja configurado.
- Owner allowlist configurado para `telegram:8413871765`.
- Evitar duplicidade de polling: se mover para VPS, parar gateway local antes de iniciar gateway remoto com o mesmo bot.

## Criterio de pronto

Uma tarefa so esta pronta quando:

- arquivos foram aplicados;
- backup existe quando havia risco;
- validacao rodou;
- erros foram registrados;
- GitHub recebeu commit, se for versionavel;
- pendencias estao claras.
