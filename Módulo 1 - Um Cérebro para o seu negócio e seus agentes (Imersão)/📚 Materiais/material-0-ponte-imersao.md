# Material 0 — Ponte da Imersão pra Claude Workstation

> **Fonte:** material da aula Pixel AI Hub (versão pós-review Cayo, 30/04)
> **Arquivo origem:** `material-0-ponte-imersao-claude-workstation-v7-2026-04-30.html`

---

# Material 0 v5 — Da Imersão ao Cérebro Operacional | Pixel AI Hub


# Na Imersão, a empresa ganhou um cérebro. Agora falta decidir onde cada pessoa trabalha.

Você já passou pelo mini curso e pela Imersão: essa é a fundação. Agora eu vou te dar uma fotografia prática de como aplicar isso no mundo real — principalmente se você também usa outras ferramentas, como Claude/Cowork, e precisa sincronizar tudo com o OpenClaw.

Agentes operando a empresa com cérebro, skills, crons e permissões.

Pessoas usando Claude sem bagunçar a memória da empresa.

Contexto preso em chats individuais.

Fale uma vez. O sistema lembra.


## O problema mudou de lugar.

Na Imersão, o foco era mostrar agentes OpenClaw rodando processos reais: segundo cérebro, skills, crons, heartbeats, segurança e multi-agentes. No dia a dia, apareceu outra necessidade: funcionários e sócios querem produzir dentro do Claude.


### Agente bom precisa de cérebro compartilhado.

O OpenClaw lê contexto, executa skills, acorda por crons, acompanha por heartbeats e entrega operação. Mas ele só fica inteligente se a memória da empresa estiver organizada.

Resumo: segundo cérebro é a fundação para agentes empresariais.


### O trabalho profundo acontece na estação de cada pessoa.

Estratégia, escrita, revisão, brainstorm, análise e decisões muitas vezes nascem no Claude/Cowork. Se isso fica preso no chat, a empresa volta a esquecer.

Resumo: precisamos conectar estação pessoal ao cérebro coletivo.


## Não é Claude versus OpenClaw. É cada um no lugar certo.

Essa é a nova imagem mental da aula. O aluno precisa entender os papéis antes de ver arquivos, templates ou comandos.


### Claude / Cowork

Estação de trabalho. Onde a pessoa pensa, escreve, decide, analisa e transforma conhecimento bruto em trabalho.

- uso individual
- produção profunda
- contexto pessoal carregado

### GitHub / Repo

Fonte de verdade. Onde o cérebro mora em Markdown, versionado, auditável, portátil e compartilhável com permissão.

- memória da empresa
- histórico de mudanças
- ponte entre ferramentas

### OpenClaw

Operação 24/7. Onde rodam captura, inbox, consolidação, crons, heartbeats, canais e agentes especializados.

- rotinas recorrentes
- execução nos canais
- follow-up e automação

## A arquitetura existe porque as alternativas quebram em algum ponto.

Aqui a aula responde a objeção antes dela aparecer. Não estamos criando pastas por estética; estamos escolhendo o arranjo que mantém contexto vivo, portável e governável.


### Só Claude solto

Rápido para a pessoa, péssimo para a empresa. O conhecimento fica preso em chats e não vira memória operacional.


### Só OpenClaw nos canais

Excelente para operação e rotina, mas nem todo trabalho profundo nasce no Telegram, Slack ou WhatsApp.


### Managed Agents isolados

Bom para começar rápido, mas sem uma fonte de verdade compartilhada cada agente vira uma ilha.


### Obsidian / Notion

Ótimo para humano organizar conhecimento. Fraco como contrato operacional se o agente não sabe onde agir e como sincronizar.


### Arquitetura proposta

Claude trabalha. GitHub versiona. OpenClaw opera. Os cérebros separam permissão e contexto.


## Os arquivos são só a superfície. O que importa são as camadas.

A versão anterior explicava a anatomia do OpenClaw. Esta versão mostra a anatomia do cérebro como infraestrutura independente de ferramenta.


### Como a pessoa trabalha

Claude/Cowork lê o contrato local e opera como copiloto do humano.


### Quem o agente é e serve

Define papel, tom, limites, usuário, empresa, prioridades e forma de resposta.


### O que precisa sobreviver

Decisões, contexto, projetos, pessoas, aprendizados e histórico consolidado.


### Como vira capacidade

Processos repetíveis e rotinas recorrentes transformam memória em execução.


### Como o agente se acha

Mapas impedem que o agente precise adivinhar onde está cada coisa.


### Como todo mundo sincroniza

GitHub mantém histórico, revisão, rollback e ponte entre estação e agente 24/7.


## A promessa não é mágica. É um loop simples.

Captura automática + consolidação assistida + sync recorrente. Essa frase deve virar mantra da aula. Aqui é o mapa aplicado; nas próximas aulas você vai ver o template abrindo, arquivos mudando, Claude trabalhando na estação e OpenClaw sincronizando a operação.


### Trabalho nasce

No Claude, em reunião, no WhatsApp, em áudio, num documento ou numa decisão.


### Captura

Claude no laptop: você fala "salva isso" e dispara /sync-pessoal , /sync-empresa ou /sync-diretoria — o destino é o comando. OpenClaw no celular 24/7: você manda áudio/texto pelo WhatsApp e o agente roteia sozinho pelas palavras.


### Inbox

Nada precisa nascer perfeito. Primeiro entra como rascunho — com origem, data e contexto bruto. O time inteiro já consegue consultar.


### Consolidação

De madrugada o agente promove o que amadureceu pra canônico (memória oficial). Algumas rotinas vão além: lêem do cérebro, executam no mundo, e escrevem aprendizado de volta.


### Recall

Na próxima execução, Claude ou OpenClaw consulta o cérebro antes de agir. Time inteiro acessa o mesmo contexto.


## Separar cérebros é separar permissão, ruído e responsabilidade.

A empresa não tem uma memória única porque nem todo mundo pode acessar tudo. A arquitetura dos 3 cérebros é uma decisão de governança.


### O que só a pessoa precisa lembrar

Preferências, rotina, ideias individuais, contexto privado, estilo de trabalho, relações e histórico pessoal. É o cérebro da estação. Alinhado com o mini-curso (mesmo modelo de workspace + git backup); ganha a skill /sync-pessoal que mantém daily notes e propaga material.


### O que o time precisa operar

Processos, projetos, clientes, aprendizados, área, FAQ, materiais, playbooks e rotinas. É o cérebro operacional.


### O que é sensível e estratégico

Dinheiro, pessoas nominais, contratos, jurídico, sócios, decisões de liderança e governança. É o cérebro de direção.


## Toda sessão começa com /cerebro .

Olha o detalhe: quando você abre o Claude na pasta da empresa, ele só enxerga o que tá direto ali. Não sabe das subpastas. /cerebro é o comando que diz: "abre os 3 cérebros pra mim" . Sem ele, o Claude fica míope.


### /cerebro

Você roda uma vez no início da sessão. Em segundos, o Claude lê os 3 cérebros — pessoal, empresa, diretoria — e fica sabendo quem é quem, quais as regras de cada um, e quem é você (sócio ou colaborador).


### Primeira coisa, sempre

Abriu o Claude na pasta da empresa? Antes de pedir qualquer coisa, roda /cerebro . É como dar bom-dia pro agente — só que ele volta sabendo de tudo que importa.


### O agente para de chutar

Sem /cerebro , "uma estação, três cérebros" é promessa de marketing. Com ele, é real. O Claude sabe o que pode mandar pra empresa, o que precisa ir pra diretoria, e o que fica só com você.


## Tem 2 momentos. Não mistura.

Um é o que você faz uma vez quando começa. O outro é o que você faz todo santo dia. Confundir os dois é o que faz curso de IA virar pesadelo de instalação.


### setup-workstation

Você roda uma vez por máquina nova . Ele faz o trabalho chato: clona os 3 templates, cria a pasta ~/{empresa}/ , instala as skills ( /cerebro , /sync-pessoal , /sync-empresa , /sync-diretoria ), confere se tá tudo no lugar. No fim, te mostra um check visual: ✓ pessoal · ✓ empresa · ✓ diretoria · ✓ /cerebro · ✓ proteção ativa. Acabou. Nunca mais mexe.


### família /sync-* + /cerebro

Você abre o Claude na pasta da empresa, roda /cerebro , e começa a trabalhar. Fala em português normal: "salva isso", "manda pra empresa", "isso aqui é da diretoria". Fim do dia, /sync-pessoal fecha tudo. Sem terminal, sem comando estranho, sem servidor pra configurar.

Esse é outro momento, em outro lugar. Quando você for ligar o agente do time (Léo) ou da diretoria (Aurora), aí roda setup-agente-openclaw — wizard separado, no servidor onde o agente vai morar. Não mistura com o setup do seu laptop. Cada um na sua casa.


## O agente não consegue salvar nada sozinho.

Eu já vi isso quebrar feio: agente animado, sai distribuindo arquivo nos cérebros sem permissão, mistura material privado com material da empresa. Solução não é confiar mais no agente — é tirar a capacidade dele agir sozinho.

Os repos vêm com uma trava no commit . Quem chega tentando salvar bate na trava. Não passa.

Só as skills oficiais ( /sync-pessoal , /sync-empresa , /sync-diretoria ) sabem destravar — e elas precisam ser chamadas por você .

Resultado: erro do agente fica impossível por construção , não por confiança.


## A ferramenta muda. O cérebro fica.

O aluno termina entendendo por que a aula existe depois da Imersão, por que essa arquitetura é recomendada e como Claude, GitHub e OpenClaw se encaixam.
