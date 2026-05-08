# Case Chris (Everest) — outbound híbrido digital + físico

> Raspa restaurantes por cidade, gera menu web melhor como prova personalizada, envia postcard físico pro dono. Outbound criativo no piloto automático.

---

## Quem opera

**Chris** · founder do Everest · ferramenta de melhoria de menu para restaurantes (mercado internacional).

Modelo: vende serviço de redesign de menu web pra restaurantes pequenos. Desafio: outbound em escala pra dono de restaurante (público não-tech, baixa resposta a email frio).

---

## O fluxo automático

### 1. Scraping (digital)
Agente raspa Google Maps + Yelp pra mapear restaurantes por cidade-alvo:
- Nome do restaurante
- Endereço
- Site atual (se tiver)
- Rating + número de reviews
- Telefone/email se disponível

### 2. Geração de prova (digital)
Pra cada restaurante mapeado:
- Lê menu atual (PDF/foto/site)
- Gera **versão web melhorada** do menu (UI moderna, fotos, categorização clara)
- Hospeda em URL única tipo `everest.com/r/<restaurante-id>`
- Personaliza com nome do restaurante, fotos reais, paleta de cores

### 3. Postcard físico
Pra cada restaurante alvo:
- Gera **postcard físico** com:
  - Foto do restaurante na frente
  - QR code pro menu redesenhado
  - Mensagem curta personalizada
- API de impressão postal (Lob ou similar) imprime + envia
- Custo: ~US$ 1.50 por postcard

### 4. Tracking
- QR code no postcard tem UTM único
- Quando dono escaneia → analytics dispara
- Agente sabe quem viu, quando, e dá follow-up via email automático

---

## Por que funciona

Restaurante recebe postcard físico no correio com **menu DELE** já redesenhado. Não é pitch. É prova de valor. Conversão alta porque:

- Postal físico tem ~10-30x mais open rate que email frio
- Personalização real (não "olá restaurante!")
- Prova de capacidade antes de pitch (vê o resultado ANTES de pagar)
- Custo baixo por touch (postcard + scrape automatizado)

---

## Stack

- **OpenClaw Managed Hostinger**
- **Skills custom:** scrape-restaurants, redesign-menu, generate-postcard, track-qr-clicks
- **Integrações:** Google Maps API, Yelp API, Lob (impressão postal), Stripe (cobrança), Postmark (email follow-up)
- **Crons:** scrape diário (50 restaurantes/dia), envio de postcards 3x/semana, follow-up automático
- **Modelo:** Claude Sonnet 4.5 (custo otimizado)

---

## Resultado mensurável

- **Volume:** 150-200 postcards/mês enviados
- **Conversão:** ~12% scan-to-call (vs ~2% típico de email frio)
- **Conversão final:** ~3% sale (postcard → cliente pagante)
- **Custo por aquisição:** ~US$ 50 (postcard + API + agente)
- **Ticket médio:** US$ 297/mês (assinatura)
- **Custo total da operação:** ~R$ 1.500/mês
- **ROI:** ~6x (5 vendas/mês × US$ 297 = US$ 1.485)

---

## Lições replicáveis

### O que QUALQUER aluno pode aplicar

1. **Outbound criativo + agente = escala** — automação de outbound não-óbvio (postcard) é diferencial
2. **Prova de valor antes de pitch** — restaurante vê o menu redesenhado ANTES de pagar
3. **Mistura digital + físico** — agente operando até carta postal expande criatividade
4. **Skills custom de domínio** — `redesign-menu`, `generate-postcard` são únicas do Chris. Inventou via `criar-skill`

### Onde NÃO replica direto

- Mercado internacional ajuda (postcard é mais comum nos EUA/Europa)
- Custo por touch precisa ser sustentável pelo ticket médio
- Setup de impressão postal API é específico (Lob é US-based)

---

## Insight crítico

> Outbound digital virou commodity. Agente bom atua onde concorrente não atua: **fronteira do digital com o físico**.

Postcards · cartas escritas à mão · brindes personalizados · presentes físicos com tracking. Tudo automatizável com agente + APIs certas.

---

## Onde ver mais

- Skill `criar-skill` (cheatsheet `skills-do-seu-agente.md`) ensina a criar skills domain-specific
- Aula E3 (Cases PME) da Hotmart cita o Chris como inspiração
- Cheatsheet `integracoes-de-produtividade.md` cobre conectar APIs externas (Google Maps, Lob)

---

📌 Atualizado em 04/05/2026 · Pixel Educação
