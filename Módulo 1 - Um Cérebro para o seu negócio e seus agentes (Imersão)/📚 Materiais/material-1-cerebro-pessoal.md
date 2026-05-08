# Material 1 — Cérebro Pessoal

> **Fonte:** material da aula Pixel AI Hub (versão pós-review Cayo, 30/04)
> **Arquivo origem:** `material-1-cerebro-pessoal-v6-2026-04-30.html`

---

# Material 1 v4 — Cérebro Pessoal (pré-requisito mini-curso) | Pixel AI Hub


# Agora a IA começa a lembrar de você.

O cérebro pessoal é a primeira estação de trabalho com memória. Nesta aula, você vai ver a ativação real — sem virar uma lista cega de comandos: o que cada passo faz, por que ele existe, onde o arquivo muda e como provar que funcionou.


## Promessa da aula

Você já configurou o workspace organizado + git backup no mini-curso OpenClaw . Aqui só ativamos a skill /sync-pessoal que automatiza pull/push e ensina o Claude sobre suas pastas.

Resultado esperado: Claude entende sua estrutura sem você explicar toda sessão; OpenClaw pessoal mantém workspace sincronizado.

Ideia central: seu contexto vive nos seus arquivos versionados no GitHub. A skill é só o automatismo de pull/push e orientação. Você fala "salva isso" em linguagem natural — não decora comando.

Na prática: você aponta o repositório, ativa /sync-pessoal , fala "salva isso" durante o trabalho e testa recall em nova sessão. Eu vou mostrar tudo isso ao vivo.


## O pessoal vem antes do coletivo.

Começar pelo cérebro pessoal reduz a complexidade. Primeiro você aprende o básico: dar contexto ao seu próprio agente, salvar uma memória real e testar se ela aparece em outra sessão.


### Menos permissão

Uma pessoa escreve. Uma pessoa usa. Sem PR, sem aprovação, sem política complexa.


### Mais identificação

Você vê o agente aprendendo quem você é, como trabalha e quais frentes toca.


### Memória portátil

O contexto fica em Markdown/HTML e Git. Claude Cowork e OpenClaw podem usar a mesma fonte de verdade.


### Primeira prova

Depois de salvar contexto, você testa em uma nova sessão do Claude ou no OpenClaw. É o momento “caramba, isso funciona”.


## Do template vazio ao agente lembrando.

A aula deve ser mão na massa, mas sem virar lista cega de comandos. Cada passo precisa responder: o que estou fazendo, por que isso existe e como sei que funcionou? A tela precisa mostrar o agente criando arquivos, explicando o diff e testando recall.


### Entender

O cérebro pessoal é a estação individual com memória.

Ele guarda contexto, rotinas e skills do dono.


### Usar template

Você entrega o template ao co-work.

Ele mostra o que vai criar antes de mexer no repo.


### Ativar /sync-pessoal

Você instala a skill /sync-pessoal no Claude/Cowork.

Ela faz pull no início, lê CLAUDE.md/MAPA.md, push no fim — invisível pro usuário.


### Conectar OpenClaw

O OpenClaw aponta para o mesmo repo.

Ele usa o cérebro fora da sessão local: canais, capturas e rotinas.


### Salvar em linguagem natural

Você fala "salva isso" , "comita" , "guarda" .

Não tem skill formal — Claude entende e commita. Hook anti-commit-autônomo garante que só commit explícito do humano passa.


### Testar recall

Abra uma nova sessão e peça para usar a memória salva.

Se o agente encontra sem você repetir tudo, a infraestrutura ligou.


## Não é uma pasta de arquivos. É o ambiente do agente.

A explicação importante: cada arquivo existe para reduzir uma pergunta que o agente faria de novo. A estrutura abaixo é uma base, não uma regra universal.


### Anatomia do cérebro pessoal

CLAUDE.md instrui a estação de trabalho.

MAPA.md mostra onde procurar.

agentes/ define quem é o agente e quem ele serve.

empresa/contexto/ guarda conhecimento pessoal sobre a empresa.

content/ , projects/ , people/ e ideas/ podem existir conforme o uso.

empresa/skills/ transforma processo repetido em capacidade.

Veja ao vivo: o aluno vê cada arquivo sendo criado/alterado pelo co-work, não por linha de comando. A promessa não é “confia”; é abrir o arquivo e mostrar o que mudou.


## O cérebro da Amora cresceu com uso real.

Este bloco mostra como a pasta de uma pessoa que usa há muito tempo fica organizada. Não é template, não é estrutura recomendada. Olha como inspiração — o seu workspace pessoal vai ser do jeito que VOCÊ aprendeu a montar no mini-curso.


### Workspace pessoal cresce com uso

Começa simples. Conforme você usa, descobre que precisa separar áreas, projetos, pessoas, ideias.

Cada pessoa quebra a estrutura conforme a operação dela.

No exemplo da Amora abaixo: tem áreas pra conteúdo, projetos, pessoas, integrações, reports, skills. Mas isso é o que faz sentido pra ela.


## O cérebro mora no repo. A ferramenta só abre a porta.

Para esta aula, pense em duas portas principais: Claude/Cowork como estação de trabalho e OpenClaw como agente sempre ligado. Os dois precisam apontar para o mesmo repositório de memória.


### Estação de trabalho

É onde você trabalha: escreve, pergunta, revisa material, toma decisão e pede ao agente para salvar o que importa. O CLAUDE.md orienta essa estação.


### Agente sempre ligado

É o ambiente que pode receber mensagens, capturar por linguagem natural, rodar rotinas e manter continuidade fora da sessão local. Ele também precisa carregar mapa, memória, contexto, rotinas e skills.


### Fonte de verdade

O GitHub é a ponte entre estação local e OpenClaw. O aluno não precisa operar terminal: ele aponta o repositório e pede ao agente para clonar, salvar ou sincronizar.


## Primeiro liga a estação. Depois liga o OpenClaw.

O feedback importante: não basta inicializar o Claude/Cowork. Se o OpenClaw também vai usar esse cérebro, a aula precisa mostrar como ele encontra o mesmo repo e carrega as mesmas regras.


### 1. Ativar /sync-pessoal no Claude/Cowork

A skill /sync-pessoal (instalada via mini-curso) é responsável por: pull automático do seu repo no início da sessão, ler CLAUDE.md / MAPA.md pra orientar Claude, e push no fim.

Prova: abrir Claude no workspace, ver "puxando última versão do GitHub", ver mapa carregado.


### 2. OpenClaw pessoal aponta pro mesmo repo

O OpenClaw pessoal (laptop ou VPS, da decisão do aluno) também aponta pro mesmo repositório. Cron de pull/push mantém workspace sincronizado entre ambientes. Não precisa skill nova — git puro.

Prova: mandar "salva isso" no Telegram do agente, abrir laptop, ver arquivo no repo já sincronizado.


## Cada arquivo responde uma pergunta diferente.

A confusão comum é colocar tudo no mesmo escopo. O cérebro é o conjunto de arquivos; estes três arquivos só orientam como o agente deve entrar, agir e se comportar.


### CLAUDE.md

Manual da estação de trabalho: onde olhar, o que ler antes de agir e como salvar decisões.


### SOUL.md

Define a persona do agente: tom, postura, critérios de decisão e jeito de trabalhar.


### AGENTS.md

Define regras gerais do ambiente quando o agente roda no OpenClaw ou em contexto multiagente.


## Tem mais coisa pronta do que parece.

O repo pessoal não entrega só pastas. Ele precisa nascer com o mesmo padrão que aparece no cérebro da Amora: contexto , rotinas e skills . A diferença é escala, não princípio.


### /sync-pessoal

Skill do template pessoal do Hub, alinhada com o que o mini-curso ensina (mesma mecânica). Faz pull automático do seu repo pessoal no início da sessão Claude/Cowork, lê CLAUDE.md / MAPA.md pra orientar o agente, mantém daily notes em agentes/{slug}/memory/YYYY-MM-DD.md , e push no fim.


### "salva isso", "comita"

No meio do trabalho, você fala em linguagem natural — Claude entende e commita no workspace pessoal. O hook anti-commit-autônomo garante que só commit explícito do humano passa.


### /sync-empresa, /sync-diretoria

Material vira parte de algum cérebro coletivo? Use as skills do Hub (Material 2 e 3). Elas ficam dentro dos repos coletivos. Pessoal nunca vaza pra coletivo automaticamente.


### Claude Code mobile

Você abre Claude Code no celular e fala "salva isso pra empresa" — a skill /sync-* roda na sessão mobile mesmo. Allowlist + linguagem natural valem. OpenClaw nunca distribui cross-brain — esse fluxo passa sempre por sessão Claude com humano no loop.


## O pessoal é simples porque é individual.

Essa parte evita expectativa errada. O template pessoal é direto em main e não replica a arquitetura coletiva.


### Só main

Não tem PR, staging ou consolidação noturna. O dono escreve direto no próprio cérebro.


### Não é coletivo

Não existe inbox interno porque não há vários membros escrevendo. O que vira coletivo sai via /sync-empresa ou /sync-diretoria (skills do Hub).


### Markdown e HTML

Markdown e HTML entram direto no cérebro. Para PDF, PPTX, XLSX, imagem ou vídeo, suba uma versão em Markdown e registre o link do original no Drive, Notion ou outra fonte.


## Você não começa do zero — e não precisa abrir terminal.

Você recebe o template. Seu trabalho é apontar o repositório para o co-work e pedir que ele transforme o template genérico no seu cérebro pessoal, mostrando os arquivos que mudam.


### 1. Apontar o template

Envie o link do repositório oficial do Pixel AI Hub e peça ao co-work para criar seu cérebro pessoal.

O nome ideal carrega empresa + agente/dono. Exemplo: acme-bruno , pixel-amora , minhaempresa-founder .


### 2. Não tem inicialização aqui

O cérebro pessoal não tem template do Hub — você já organizou no mini-curso. Aqui basta ter CLAUDE.md + MAPA.md na raiz pra orientar o Claude. O resto da estrutura é do jeito que VOCÊ aprendeu a montar.

O objetivo não é seguir um template — é o agente entender o seu jeito de organizar e te ajudar a manter sincronizado entre laptop e VPS.


## O aluno precisa ver o co-work fazendo, não ouvir teoria.

Aqui entra a tela ao vivo: template aberto, co-work recebendo o pedido, arquivos sendo criados/alterados, primeiro save funcionando e nova sessão provando recall. Essa é a ponte real entre a Imersão e o cérebro pessoal.

Colar o link do template pessoal no co-work.

Pedir inicialização guiada e responder só dados faltantes.

Mostrar CLAUDE, SOUL, USER, MEMORY e MAPA preenchidos.

Dizer “salva isso” com uma decisão real.

Abrir o arquivo criado para provar que a conversa virou memória pessoal.

Abrir nova sessão e pedir para usar a memória salva.


## O mínimo que liga o cérebro.

Essa é a checklist embutida da aula. Se você fizer só isso, já tem um cérebro pessoal funcional para testar.

Troque {FUNDADOR_1} pelo seu nome — a pessoa que vai usar esse cérebro.

Preencher empresa, slug e contexto básico do negócio.

Definir {AGENTE_NOME} e {AGENTE_SLUG} para o assistente pessoal.

Quem você é, como trabalha, idioma, preferências e objetivos.

Como o agente deve se comportar: direto, proativo, técnico, comercial, etc.

Conferir se os caminhos principais fazem sentido depois da inicialização.

Adicionar o mínimo sobre produto, clientes, prioridades e pessoas importantes.

Salvar uma decisão ou preferência real para testar memória depois. Você não decora comando: escreve "salva isso" , "guarda isso" ou "lembra disso" .


## Do chat à memória consultável.

Esse é o fluxo que precisa ficar claro: você trabalha, pede para salvar, o repo muda, GitHub sincroniza e uma nova sessão consegue usar o mesmo contexto.

Você trabalha com o agent normalmente: estratégia, decisão, reunião, ideia ou plano.

Você fala em linguagem natural durante o trabalho. Claude commita no workspace pessoal.

Daily note e contexto durável são atualizados em memory/ e empresa/contexto/ .

O agente salva e sincroniza a memória no repositório. O aluno não precisa digitar comandos.

Estação de trabalho e OpenClaw passam a olhar para a mesma fonte de verdade.

Em nova sessão, o agente consulta a memória antes de responder.


### Não decore comandos. Entenda as skills.

Para o aluno, isso deve parecer simples: /sync-pessoal automatiza pull/push e ensina o Claude sobre suas pastas. Você fala "salva isso" em linguagem natural quando quer commitar. /sync-empresa e /sync-diretoria (Materiais 2 e 3) são as skills do Hub que propagam pros cérebros coletivos. Claude/Cowork é a estação de trabalho; OpenClaw é o agente sempre ligado que também usa esse cérebro.


## O cérebro não é abstrato. Ele vira arquivo.

Depois da skill save, você deveria conseguir abrir o repo e enxergar a memória materializada — junto com as perguntas que o agente fez para não salvar no lugar errado. Algo assim:


### O que mudou no repo

Um checkpoint simples pode atualizar duas camadas: diário da sessão e contexto durável.


## Sem teste, é só pasta bonita.

O teste precisa ser simples: salvar algo uma vez, abrir nova sessão e ver o agente usar o mesmo contexto. A prova não é só “lembrar”; é não precisar explicar tudo de novo.


### O “aha moment” é ver o arquivo nascer.

Você não precisa confiar na promessa. Você precisa ver o mesmo contexto sair de uma conversa, virar arquivo no GitHub e aparecer em uma nova sessão.

Se Claude Cowork e OpenClaw conseguem usar o mesmo cérebro, a memória deixou de ser da ferramenta. Virou infraestrutura.


## O cérebro cresce por captura, não por organização perfeita.

Você não deve tentar preencher a vida inteira no primeiro dia. O cérebro pessoal melhora conforme você usa, salva manualmente o que importa e mantém o repo sincronizado.


### Quando decidir algo

Salvar o quê, por quê, contexto e trade-off.


### Quando corrigir o agente

Transformar correção recorrente em memória.


### Quando iniciar uma frente

Criar contexto mínimo: objetivo, status, próximos passos.


### Quando sair de call

Registrar aprendizados, compromissos e pendências.


## O cérebro pessoal precisa sair da conversa.

O aluno não precisa criar cron nesta aula. O que ele precisa entender é: fale "salva isso" em linguagem natural quando algo importante acontecer e mantenha o repositório no GitHub como fonte portátil. A skill /sync-pessoal cuida do pull/push automático.


### Fonte portátil

O repo vira a cópia confiável do contexto. Você consegue levar o cérebro para outra máquina, outra IA ou outro agent.


### Quando algo importa

O CLAUDE.md já orienta salvar durante o trabalho. Reforce o hábito: decidiu algo, corrigiu o agente ou fechou uma reunião? Peça para salvar.


### Sem mágica invisível

Se houver conflito, o sync deve alertar em vez de tentar resolver sozinho. Contexto é memória: não pode ser sobrescrito no escuro.


### Rotina mental do aluno

O detalhe técnico de sync pode ser automatizado depois. Nesta aula, o essencial é criar o hábito de salvar e validar recall.


### Regra importante: pessoal não é lixeira.

O cérebro pessoal é rápido porque tem dono único e portabilidade máxima. Mas nem tudo deve ficar só nele. Se uma informação precisa virar operação do time, você usa /sync-empresa . Se é sensível de liderança, usa /sync-diretoria . Cada uma é uma skill separada do Hub que vive no repo correspondente.


## O pessoal captura. O coletivo recebe só o necessário.

Você começa no pessoal porque é simples, mas precisa entender a ponte com os outros cérebros.


### Só você precisa saber

Preferências, reflexões, rotina individual, ideias ainda cruas.


### É sensível

Sócios, dinheiro, contrato, jurídico, pessoa nominal, decisão de liderança.


### O time opera

Processo, cliente, área, tarefa recorrente, aprendizado compartilhável.


## Seu agente não ficou mais inteligente. Ele ficou menos amnésico.

Essa é a mensagem final: a qualidade da IA melhora quando ela para de começar do zero. O cérebro pessoal transforma contexto individual em memória consultável, versionada e portátil.


## O que tá rodando debaixo do capô do cérebro pessoal.

Você não precisa entender pra usar — mas vale saber que existe. São 2 mecanismos pequenos que evitam dor de cabeça grande.


### /cerebro

Quando você abre o Claude na pasta da empresa (vai virar hábito), /cerebro é a primeira coisa. Em segundos, ele carrega os 3 cérebros e o agente sabe quem é quem. Aqui no pessoal sozinho até dá pra pular , mas vira costume bom — você nunca esquece quando trabalhar com mais de um.


### Agente não salva sozinho

Tem uma trava no repo: nada é salvo automaticamente . Só skills oficiais (tipo /sync-pessoal ) destravam — e elas precisam ser chamadas por você. Mesmo no seu cérebro pessoal, a regra vale. Erro de agente fica impossível por construção, não por confiança.
