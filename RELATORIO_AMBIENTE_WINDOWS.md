# Relatorio do Ambiente Windows para OpenClaw

Data/hora da auditoria: 2026-05-08 14:47:24 -03:00  
Maquina auditada a partir de: `C:\Users\aliss\OneDrive\Desktop\Open Claw`

## 1. Sistema operacional

- Windows: Microsoft Windows 11 Pro
- Versao: 10.0.26200
- Build: 26200
- Arquitetura: 64 bits
- Ultimo boot: 2026-05-08 14:30:20

## 2. PowerShell

- PowerShell: 7.6.1
- PSEdition: Core
- Platform: Win32NT

Status: adequado para instalacao por npm/PowerShell.

## 3. Ferramentas instaladas

| Ferramenta | Status | Versao / observacao |
|---|---:|---|
| Git | OK | `git version 2.53.0.windows.2` |
| Node.js | OK | `v24.14.1` |
| npm | OK | `11.11.0` |
| pnpm | OK | `10.33.2` |
| Python | OK parcial | `Python 3.14.4` via WindowsApps |
| pip | Faltando | `pip` nao encontrado no PATH |
| Docker | Faltando | `docker` nao encontrado |
| Docker Compose | Faltando | depende de Docker |
| WSL | Faltando | `wsl.exe` existe, mas WSL nao esta instalado |
| OpenClaw CLI | Faltando | `openclaw` nao encontrado |
| GitHub CLI (`gh`) | Faltando | opcional para backups/sync GitHub |
| curl | OK | `curl 8.18.0 (Windows)` |

## 4. Node/npm

- Prefixo global npm: `C:\Users\aliss\AppData\Roaming\npm`
- Global node_modules: `C:\Users\aliss\AppData\Roaming\npm\node_modules`
- O PATH contem:
  - `C:\Program Files\nodejs\`
  - `C:\Users\aliss\AppData\Roaming\npm`

Status: adequado para instalar `openclaw@latest` globalmente com npm.

## 5. Pacote OpenClaw no npm

Consulta executada:

```powershell
npm view openclaw name version description bin dist-tags engines --json
```

Resultado relevante:

- Pacote: `openclaw`
- Versao mais recente: `2026.5.7`
- Binario: `openclaw`
- Engine: `node >=22.14.0`
- Node instalado: `v24.14.1`

Conclusao: o ambiente Node atende ao requisito do pacote atual.

## 6. Docker e WSL

Docker nao esta instalado. WSL tambem nao esta instalado.

Isso nao bloqueia o metodo de instalacao por npm global no Windows. Bloquearia apenas cenarios que dependem de Linux, containers, `systemctl` ou instalacao via script Bash.

## 7. Variaveis de ambiente relevantes

Foram encontradas variaveis relevantes:

| Variavel | Status |
|---|---|
| `OPENAI_API_KEY` | presente, valor mascarado |
| `CODEX_MANAGED_BY_NPM` | presente |
| `WSLENV` | presente |

Nenhuma chave foi exibida em claro.

## 8. Portas em uso

Portas comuns verificadas: `80`, `443`, `3000`, `3001`, `4000`, `5000`, `5173`, `5432`, `6379`, `8000`, `8080`, `8081`, `8787`, `11434`.

Resultado: nenhum listener nessas portas foi detectado no momento da auditoria.

## 9. Pastas de estado

| Path | Status |
|---|---|
| `C:\Users\aliss\.openclaw` | nao existe |
| `C:\Users\aliss\.config` | existe, contem `configstore` |
| `C:\Users\aliss\.codex` | existe, contem estado do Codex, nao OpenClaw |

`C:\Users\aliss\.codex` nao sera alterado por esta instalacao.

## 10. Permissoes da pasta auditada

Pasta: `C:\Users\aliss\OneDrive\Desktop\Open Claw`

Owner: `ATIMO\aliss`

Permissoes relevantes:

- Usuario `ATimo\aliss`: FullControl
- Administradores/SYSTEM: FullControl
- CodexSandboxUsers: Modify
- Existe uma regra `Everyone Deny DeleteSubdirectoriesAndFiles`, o que ajuda contra remocoes acidentais.

Status: leitura e criacao de relatorios/backup estao permitidas.

## 11. Processos relacionados

Foram encontrados varios processos `node.exe`, ligados ao ambiente Codex/OpenAI, mas nenhum processo `openclaw` foi encontrado.

## 12. Conclusao do ambiente

O computador esta pronto para a instalacao base do OpenClaw via npm global:

```powershell
npm install -g openclaw@latest
```

Pendencias nao bloqueantes:

- `pip` nao encontrado.
- Docker nao instalado.
- WSL nao instalado.
- `gh` CLI nao instalado.

Pendencia funcional provavel:

- Onboarding do OpenClaw pode exigir autenticacao humana e escolhas de provider/modelo/canais. Eu nao devo inventar tokens, senhas, chaves nem respostas pessoais.

## 13. Atualizacao pos-instalacao

Status atualizado em 2026-05-08 15:00 -03:00.

Resultado da instalacao:

- `openclaw@latest` instalado via npm global.
- Versao instalada: `OpenClaw 2026.5.7`.
- `openclaw config validate`: valido.
- `openclaw gateway status`: gateway local alcancavel em `ws://127.0.0.1:18789`.
- Dashboard: `http://127.0.0.1:18789/`.
- `Invoke-WebRequest http://127.0.0.1:18789/`: HTTP `200`.
- Processo listener: `node.exe` em `127.0.0.1:18789`.
- Teste de agente local: sucesso com resposta `OK_OPENCLAW`.

Estado atual:

- CLI instalada e funcional.
- Workspace criado em `C:\Users\aliss\.openclaw\workspace`.
- Gateway rodando como processo manual, iniciado via `C:\Users\aliss\.openclaw\gateway.cmd`.
- Scheduled Task nao foi criada por falta de permissao (`Acceso denegado`).

Pendencias de ambiente:

- Para persistencia apos reboot, rodar `openclaw gateway install` em PowerShell com permissao adequada ou usar WSL2 conforme recomendacao oficial do proprio OpenClaw para Windows.
- Telegram foi configurado depois desta auditoria com `TELEGRAM_BOT_TOKEN` no escopo de usuario.
- `gh`, Docker, WSL e pip continuam ausentes; nenhum deles foi necessario para a instalacao base.

## 14. Atualizacao Telegram/OpenAI

Status atualizado em 2026-05-08 15:25 -03:00.

- Historico inicial: `OPENAI_API_KEY` estava presente e funcional; antes da correcao OAuth, o teste do agente usou provider `openai`, modelo `gpt-5.5`.
- Estado atual: ver secao 17; a Esperancita usa `openai-codex/gpt-5.5` via OAuth para conversas.
- `TELEGRAM_BOT_TOKEN`: presente no escopo de usuario e processo; valor omitido.
- `openclaw channels status --probe`: Telegram configurado, rodando e conectado em modo `polling`.
- Bot Telegram validado: `@esperancitamy_bot`.
- Gateway continua local em `127.0.0.1:18789`.
- Scheduled Task continua pendente por permissao; gateway esta rodando como processo manual.

## 15. Atualizacao de pareamento Telegram

Status atualizado em 2026-05-08 15:37 -03:00.

- Pedido de pareamento recebido pelo Telegram.
- Remetente aprovado.
- `commands.ownerAllowFrom` configurado automaticamente pelo OpenClaw.
- Teste de envio direto Telegram retornou `ok=true`.
- Teste de agente com OpenAI e entrega no Telegram retornou `deliverySucceeded=true`.
- Nenhuma configuracao de Hostinger ou GitHub foi feita.

## 16. Atualizacao Hostinger API

Status atualizado em 2026-05-08 15:45 -03:00.

- `HAPI_API_TOKEN`: configurado no escopo de usuario. Em cada novo PowerShell, importar com `$env:HAPI_API_TOKEN = [Environment]::GetEnvironmentVariable('HAPI_API_TOKEN', 'User')` antes de usar.
- Valor do token omitido.
- `openclaw.json` nao contem o token literal.
- API Hostinger respondeu ao endpoint somente-leitura de VPS.
- Foram encontradas 2 VPS `KVM 2`.
- Hospedagem do OpenClaw na Hostinger ainda nao foi executada.
- GitHub continua sem token/configuracao.

## 17. Atualizacao OpenAI OAuth da Esperancita

Status atualizado em 2026-05-08 16:03 -03:00.

- OAuth ChatGPT/OpenAI Codex configurado via terminal interativo.
- Perfil OAuth salvo em `C:\Users\aliss\.openclaw\agents\main\agent\auth-profiles.json`.
- Modelo padrao do agente: `openai-codex/gpt-5.5`.
- Modelos permitidos do agente: somente `openai-codex/gpt-5.5`.
- `OPENAI_API_KEY` continua presente no ambiente para transcricao/Whisper.
- Teste de entrega Telegram via agente confirmou `provider=openai-codex`.
