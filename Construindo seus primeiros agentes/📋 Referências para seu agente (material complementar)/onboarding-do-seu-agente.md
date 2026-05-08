---
name: onboarding-do-seu-agente
status: ATIVO
category: cheatsheet
referenced_by: [A1]
version: 1.0
last_updated: 2026-05-04
description: Cheatsheet pra setup inicial do agente OpenClaw Managed (A1). Cobre Fase A (credencial OpenAI API + crédito) · Fase B (OAuth ChatGPT via terminal) · Quick Win Telegram (Bloco 5 da A1) · prompt de onboarding canônico · 4 prompts prontos pra colar · troubleshooting comum.
---

# Onboarding do seu agente — referência rápida (A1)

## A1 em 1 minuto (resumo executivo)

Setup completo do agente OpenClaw Managed = **2 credenciais complementares** + **2 canais de fala** + **1 prompt de auto-conhecimento**:

| Etapa | O que faz | Onde |
|-------|-----------|------|
| **Fase A — Credencial OpenAI API** | Autentica OpenClaw + libera Whisper · embeddings · memória semântica | platform.openai.com (NÃO chatgpt.com) |
| **Fase B — OAuth ChatGPT Plus** | Destrava GPT 5.5/5.4 da assinatura · economiza crédito da API | Terminal Managed (1 comando) |
| **Bloco 5 — Telegram DM** | Habilita Quick Win da A4 (zip do kit não cabe no Gateway) | @BotFather + comando `channels add` |
| **Onboarding prompt** | Agente lê llms-full.txt e cria MEMORY.md de auto-conhecimento | DM ou painel |

## Fase A — Configurar credencial OpenAI API

### 1. Criar conta no `platform.openai.com` (NÃO `chatgpt.com`)

| Site | Pra que serve |
|------|---------------|
| **`platform.openai.com`** ⭐ | API + créditos pré-pagos · Whisper · embeddings · gera API key |
| `chatgpt.com` | Assinatura ChatGPT Plus (pra OAuth da Fase B) |

**Diferença crítica**: aluno PME confunde direto. Site errado = não consegue gerar API key.

### 2. Cadastrar cartão + comprar crédito (US$ 5-10 inicial)

- Painel OpenAI → Settings → Billing → Add payment method
- Compra US$ 5-10 de crédito inicial
- **Por que esse valor**: cobre Whisper + embeddings + memória semântica por meses pra aluno PME normal

### 3. Gerar API key

- Painel OpenAI → API Keys → Create new secret key
- Copia · cola num lugar seguro
- Princípio (recap A10): NÃO compartilha · NÃO commita em GitHub público

### 4. Contratar Managed OpenClaw + cupom BRUNOOKAMOTO

- Landing: [hostg.xyz/SHJMI](https://www.hostg.xyz/SHJMI)
- Aplicar cupom **BRUNOOKAMOTO**
- Aguardar provisionamento (3-5min)

### 5. Logar painel OpenClaw com API key

- Acessa painel Hostinger → menu OpenClaw → seu OpenClaw
- Cola API key no campo solicitado
- Painel ativa · agente já consegue responder usando modelo da API

## Fase B — Ativar OAuth ChatGPT (segundo passo crítico)

### 1. Abrir terminal Managed pela primeira vez

- Painel Hostinger → menu OpenClaw → seu OpenClaw → **"Abrir linha de comando (CLI)"**

### 2. Rodar comando OAuth

```bash
openclaw models auth login --provider openai-codex --set-default
```

### 3. Validar Fase B

```bash
openclaw models auth list   # mostra providers configurados
openclaw status              # confirma que codex provider tá default
```

## Por que as 2 fases são complementares

| Credencial | Cobertura | Custo |
|-----------|-----------|-------|
| **API key OpenAI** (Fase A) | Whisper · embeddings · memória semântica · cai aqui se OAuth falhar | Pago via crédito pré-pago (US$ 5-10) |
| **OAuth ChatGPT Plus** (Fase B) | GPT 5.5/5.4 pra inferência principal · agentic tasks | Já incluso na assinatura ChatGPT Plus (R$ 100/mês) |

**Frase-mãe da A1:** *"API key autentica seu OpenClaw e libera Whisper + embeddings. OAuth dá acesso ao GPT 5.5 da sua subscription. Você precisa das duas — uma não substitui a outra."*

## Bloco 5 — Conectar Telegram pro Quick Win

### Setup em 5 passos (~2min)

1. Abre `@BotFather` no Telegram (https://t.me/BotFather)
2. Digita `/newbot` → escolhe nome amigável + handle único
3. BotFather retorna o token (formato `123456:ABC-DEF...`) — copia
4. No terminal Managed, cola:
   ```bash
   openclaw channels add --channel telegram --token <bot-token>
   ```
5. Abre seu novo bot no Telegram, manda `/start` ou qualquer mensagem · agente responde

## Onboarding prompt canônico (Bloco 4 da A1)

Cola este prompt direto no agente **logo após Fase B completa**:

```
Leia https://docs.openclaw.ai/llms-full.txt

Em português simples me explique:
1. O que vc é e como funciona
2. O que consegue fazer hoje (canais, ferramentas, integrações)
3. O que NÃO consegue fazer (limitações reais)
4. Comandos principais que eu posso usar pra te configurar
5. Onde guarda memórias, skills, configurações e logs

Salve esse resumo em MEMORY.md como "auto-conhecimento do agente"
e me mostre o resultado.
```

## Troubleshooting comum

| Sintoma | Causa provável | Ação |
|---------|----------------|------|
| API key inválida no painel | Confundiu site (chatgpt.com em vez de platform.openai.com) | Volta em platform.openai.com → API keys → gera nova |
| OAuth via terminal trava | Browser bloqueou popup OU rede corporativa | Tenta `openclaw models auth paste-token` |
| Comando `openclaw` não encontrado | Tá em terminal local em vez de terminal Managed | Use **terminal do painel Hostinger** |
| `lshell: forbidden character` | Tentou comando bash arbitrário no Managed | Terminal Managed é lshell — só comandos `openclaw *` passam |
| Telegram bot não responde | Token errado OU bot não conectado | `openclaw channels list` → confirma · refazer `channels add` |

## Comandos `openclaw models` (validados na doc oficial)

| Comando | Pra que serve |
|---------|---------------|
| `openclaw models auth login --provider <id> [--set-default]` | OAuth ou API key — fluxo principal Fase B |
| `openclaw models auth list` | Lista providers configurados + qual é default |
| `openclaw models auth logout --provider <id>` | Desconecta provider específico |
| `openclaw models auth paste-token` | Cola token diretamente (caso OAuth visual não funcione) |

## Referências

- A1 do roteiro principal · A2 (cockpit terminal) · A3 (Telegram aprofundado) · A10 (segurança)
- [hostg.xyz/SHJMI](https://www.hostg.xyz/SHJMI) · [platform.openai.com](https://platform.openai.com)
- Doc OpenClaw `cli/models`: [docs.openclaw.ai/cli/models](https://docs.openclaw.ai/cli/models)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
