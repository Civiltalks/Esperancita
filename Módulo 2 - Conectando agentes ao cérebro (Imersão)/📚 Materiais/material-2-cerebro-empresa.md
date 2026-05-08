# Material 2 — Cérebro da Empresa

> **Fonte:** material da aula Pixel AI Hub (versão pós-review Cayo, 30/04)
> **Arquivo origem:** `material-2-cerebro-empresa-v6-2026-04-30.html`

---

# Material 2 v4 — Cérebro da Empresa | Pixel AI Hub


# Agora a empresa ganha uma memória que o time inteiro usa.

O cérebro da empresa é o repositório operacional compartilhado: marketing, vendas, atendimento, operações e produto. A aula precisa mostrar colaboração viva: duas pessoas capturando durante o dia, inbox sincronizando, OpenClaw rodando rotinas e só depois a consolidação virando memória oficial.


## Promessa da aula

Ao final, você entende o que é o cérebro da empresa, como a skill /sync-empresa propaga material do seu workspace pessoal pra inbox da empresa, e qual é o papel do OpenClaw da empresa em VPS dedicada.

Resultado esperado: o time deixa de depender da cabeça do founder pra recuperar decisões e processos.

Ideia central: 1 skill /sync-empresa que roda em sessão Claude Code (laptop ou mobile) com linguagem natural — você fala "salva isso pra empresa" e a skill propaga. Ambiguidade resolve no momento do sync , com humano no loop (não na consolidação, não em OpenClaw cross-brain).

Veja ao vivo: captura no workspace pessoal, sync pra empresa, agente da empresa em VPS dedicada consolida, time consulta sem pedir contexto ao founder.


## Uma empresa esquece quando o contexto mora nas pessoas.

No cérebro pessoal, você provou que um agente pode usar memória individual. Agora o desafio muda: fazer time e agentes trabalharem com a mesma memória operacional, sem depender de repasse manual toda semana.


### Decisões somem

Uma decisão nasce numa call, continua no WhatsApp, vira tarefa no Notion e ninguém sabe qual versão venceu.


### O founder vira roteador

Todo mundo pergunta de novo porque o contexto não está em um lugar operacional confiável.


### Agentes ficam cegos

Um agente de marketing ou vendas não consegue agir bem se precisa reconstruir a empresa a cada conversa.


### Processo não vira capacidade

Sem memória e skills, cada operação recorrente volta a ser improviso.


## O cérebro da empresa é o sistema operacional de contexto do time.

Não é uma wiki bonita. Não é drive. Não é chat. É um repo Git onde o que a empresa aprende vira arquivo, área, rotina ou skill.


### O que entra aqui

Contexto operacional: campanhas, funil de vendas, suporte, processos, roadmap, decisões de produto, playbooks, rotinas, aprendizados e materiais que o time pode acessar.

Regra prática: se ajuda o time a operar melhor e não é sensível, mora no cérebro da empresa.


### O que não entra aqui

Dinheiro com nome próprio, avaliação de pessoa, conflito, contratação, desligamento, contrato sensível, jurídico ou governança restrita.

Essas coisas pedem outro repo: o cérebro da diretoria.


## Estação de trabalho, OpenClaw e cérebro não são a mesma coisa.

Esse é o desenho que precisa ficar claro antes de falar de staging ou consolidação.


### Estação de trabalho

Claude Cowork no computador do aluno. É onde a pessoa pensa, escreve, revisa e pede para salvar contexto.


### OpenClaw da empresa

Agente sempre ligado. Recebe capturas, roda rotinas, consolida inboxes, cobra pendências e consulta o cérebro antes de agir. Na aula, precisa aparecer rodando.


### Cérebro da empresa

Repo no GitHub com a memória operacional. É a fonte de verdade que estação e OpenClaw compartilham.


## Cada cérebro existe por um motivo diferente.

Essa comparação precisa ficar cristalina. A pergunta não é “qual é melhor?”. É “quem pode ver esse contexto e para qual tipo de decisão ele serve?”.


### Cérebro pessoal

Promessa: meu agente me conhece.

- Identidade, preferências, projetos pessoais
- Uso individual
- Primeiro teste de memória
- Exemplo: “como eu gosto de responder clientes”
Promessa: o time opera com a mesma memória.

- Marketing, vendas, atendimento, operações, produto
- Uso compartilhado
- Agente operacional do time
- Exemplo: “novo processo de qualificação de leads”

### Cérebro da diretoria

Promessa: proteger o sensível.

- Financeiro nominal, RH, jurídico, governança
- Acesso restrito aos sócios
- Revisão humana obrigatória
- Exemplo: “comissão da Ana em abril”

## Do template da empresa ao primeiro contexto compartilhado.

A lógica é parecida com a aula 1, mas o papel de cada ambiente muda: a estação de trabalho captura, o cérebro da empresa guarda o operacional e o OpenClaw ajuda a consolidar a rotina.


### Entender

Você aprende que o cérebro da empresa é o repo operacional do time.

Ele guarda o que todos podem usar.


### Usar template

Você aponta o template-second-brain-empresa no co-work.

Esse repo é a base compartilhada da operação, sem linha de comando.


### Inicializar

Wizard guiado responde questionário em 3 níveis: VPS, agentes, repos, naming.

Configura branch protection + skill global no Cowork. Sem exigir terminal.


### Criar estações

Cada pessoa do time clona o repo + ganha inbox/{slug}/ próprio.

Quem só conecta (não admin): wizard detecta perfil "visitante" e configura só inbox.


### Testar colaboração

Você dá /sync-empresa ou fala "manda essa pauta pra empresa". Skill empacota + envia pra inbox + push pra GitHub.

Agente da empresa (em VPS dedicada) puxa, consolida em pastas certas, pergunta no Telegram se houver ambiguidade.


## A estrutura do cérebro da empresa segue a operação.

A arquitetura do template é simples de propósito: áreas de negócio, contexto transversal, agente gestor e inboxes de captura.


### Como ler a estrutura

areas/ organiza o conhecimento por função operacional.

empresa/ guarda princípios, arquitetura, segurança e skills gerais.

agentes/geral-empresa/ é o agente operacional do time.

inbox/ recebe capturas de humanos e diretores.

inbox → memória oficial separa captura provisória do que já virou verdade. Staging/main existem por baixo, mas o aluno precisa entender o comportamento.

OpenClaw da empresa pode rodar a rotina de consolidação, cobrar pendências e manter o cérebro vivo fora das sessões locais.


## Ele não é assistente pessoal. É operador da memória operacional.

Essa é a virada que precisa ficar explícita. A estação de trabalho é onde humanos capturam e editam. O OpenClaw da empresa é o operador de rotinas: mantém a memória viva, sincroniza sinais, consolida inboxes, cobra pendências, transforma processo repetido em skill e responde com o contexto permitido.


### Consolida

Em rotina combinada, lê capturas dos inboxes, promove o que está maduro, abre PR quando precisa revisão e arquiva o resto.


### Organiza

Mantém áreas atualizadas: marketing, vendas, atendimento, operações e produto.


### Cria capacidade

Quando um processo se repete, vira skill. A empresa deixa de depender de improviso.


### Responde com contexto

Quando alguém pergunta, ele não começa do zero: consulta o cérebro permitido e age com memória.


## O OpenClaw faz duas coisas: mantém o cérebro e opera com o cérebro.

Consolidar inbox é importante, mas não é o único papel. O agente também executa rotinas operacionais que LEEM do cérebro, agem no mundo, e ESCREVEM aprendizado de volta. Cérebro deixa de ser arquivo morto — vira substrato vivo, com camadas novas a cada dia.


### Sincronizar inboxes

Busca capturas novas, confere sidecars e aponta o que está pronto ou faltando informação.


### Consolidar memória

Promove o que amadureceu para canônico, abre PR quando precisa revisão e arquiva histórico.


### Gerar resumo

Entrega o que mudou hoje: capturas, promoções, dúvidas, conflitos e pendências.


### Cobrar pendências

Encontra capturas sem destino, decisões sem dono e processos travados.


### Criar capacidades

Quando algo se repete, propõe transformar processo em skill da empresa.


### Agente operando o cérebro — exemplo: rotina de marketing

1. LÊ DO CÉREBRO → abre areas/marketing/aprendizados.md , pega o que funcionou em campanhas anteriores. 2. EXECUTA NO MUNDO → roda 5 testes de criativo novos baseados nos aprendizados, mede performance. 3. ESCREVE NO CÉREBRO → acrescenta aprendizado novo no mesmo arquivo. Próximo ciclo já usa. O cérebro vive — cada captura humana e cada rotina autônoma vira camada nova na mesma memória.


## É um arquivo de texto. Não é cron Linux.

Aqui é onde o pessoal espera ver complicação — e é onde o sistema é mais simples. Cada rotina do agente é um arquivo. Você abre, lê, entende. Não tem servidor pra configurar, não tem orquestrador externo. É leve de propósito.


### É só isso que define uma rotina.

Durante o dia, você captura . À noite, o Léo consolida . Esse é o pacto, e ele cabe num arquivo de 6 linhas. Quem precisar do detalhe técnico (cron syntax, scope, sidecar matrix) abre o arquivo real e tá lá — mas o conceito você já pegou.


## O inbox não serve só para depois. Ele também permite o time se enxergar durante o dia.

A consolidação transforma captura em memória oficial. Mas antes disso, o inbox sincronizado já funciona como área de trabalho compartilhável: rascunho, evidência, pesquisa, regra nova e decisão em amadurecimento. Veja isso ao vivo: uma pessoa salva, outra consulta antes da consolidação.


### Bruno captura uma regra de vendas

Ele está no Claude/Cowork no workspace pessoal, decide uma regra operacional e fala "salva isso" — sem dizer destino dentro da frase. Quando quer propagar, aciona /sync-empresa em separado : a skill empacota com sidecar (autor, data, fonte, destino sugerido) e push direto pra inbox/bruno/ do repo da empresa. O destino é o comando que ele escolhe — não a frase capturada.


### Ana usa antes da consolidação

Ana ainda não precisa esperar a rotina noturna. Ela sincroniza o repo, olha o inbox e usa a captura do Bruno como contexto provisório — sabendo que é rascunho, ainda não canônico. O time inteiro acompanha em tempo real, mas só vira oficial depois da revisão noturna.


### Frase-chave da aula

Inbox sincronizado é colaboração provisória. Consolidação é memória oficial. Isso evita a falsa ideia de que o time só colabora no dia seguinte.


## Diretor conecta três cérebros. Colaborador conecta um.

Essa diferença precisa aparecer na prática, porque é onde o aluno entende permissionamento sem virar aula técnica.


### 3 cérebros

O diretor trabalha no pessoal, envia operacional para a empresa e sensível para a diretoria. Ele é a ponte humana entre os contextos.


### 1 cérebro

O colaborador usa apenas o cérebro da empresa. Ele captura no próprio inbox e consulta memória operacional permitida.


## Claude no laptop ou OpenClaw 24/7 — depende do seu dia, não da arquitetura.

A captura é a mesma ideia: você fala o conteúdo, e o cérebro certo recebe. Mas o ponto de captura muda — e isso confunde se ninguém explica. Não é uma escolha de "modo avançado"; é uma escolha de contexto físico.


### Claude no laptop

Você tá produzindo: escrevendo, decidindo, revisando. Você dispara explicitamente as skills /sync-pessoal , /sync-empresa ou /sync-diretoria . O destino é o comando que você escolhe — não a frase capturada. Visibilidade total e controle no loop.


### OpenClaw 24/7 no WhatsApp

Você tá em pé, dirigindo, na cozinha, no salão. Não dá pra abrir laptop e digitar comando. Você manda áudio ou texto pro agente OpenClaw direto no WhatsApp. O agente roteia sozinho baseado nas palavras-chave (sócio + equity → diretoria; promo + ticket → empresa; família → pessoal). É a captura do empresário em movimento.


### Pega esse exemplo: o Rafael (cliente real, dono de 2 restaurantes em Portugal).

Rafael não é técnico. O dia dele é restaurante — não tem como abrir laptop a cada captura. 8h dirigindo , fala áudio sobre viagem com a família → OpenClaw rotea pra cérebro pessoal. 11h na cozinha , fala áudio sobre uma promo de café → cérebro empresa. 16h no escritório , fala áudio sobre conversa de equity com sócio → cérebro diretoria. Mesmas 4 mensagens, 3 cérebros diferentes — sem ele decidir pasta, sem rodar comando. O OpenClaw lê as palavras e decide.


## Diretor e colaborador não fazem o mesmo caminho.

A aula precisa mostrar os dois fluxos lado a lado, porque é isso que transforma permissionamento em comportamento prático.


### Começa no workspace pessoal (mini-curso) e decide o que atravessa.

- Trabalha no Claude/Cowork no seu workspace pessoal.
- Fala "salva isso" pra commitar no pessoal naturalmente.
- Usa /sync-empresa pra enviar o operacional pro cérebro da empresa.
- Se disparar gatilho sensível, usa /sync-diretoria em vez (não vai pro time).

### Trabalha direto no workspace pessoal e propaga pra empresa.

- Tem workspace pessoal próprio (mini-curso) + repo da empresa clonado em ~/{empresa}/empresa/ .
- Captura no workspace, fala "salva isso" naturalmente.
- Usa /sync-empresa pra publicar pro inbox dele no repo da empresa.
- Consulta memória operacional + capturas provisórias permitidas.

## Gestor escreve canônico. Visitante passa pelo inbox.

Essa regra evita bagunça. O time não edita a memória oficial direto. O agente da empresa é o gestor; humanos e diretores são visitantes do canônico.


## Captura primeiro. Sync durante o dia. Consolidação depois.

Ninguém precisa virar bibliotecário. A pessoa captura durante o trabalho; o /sync-empresa publica no staging quando ela quer compartilhar; o time pode consultar o inbox provisório; o OpenClaw consolida depois o que vira memória oficial.

Call, pesquisa, reunião, brainstorm, decisão, rascunho.

Em linguagem natural durante o trabalho, Claude commita no workspace pessoal.

Quando você quer propagar pro time, dispara skill (manual ou via gatilho natural). Empacota + push pra inbox/{slug}/ do repo da empresa, pergunta no Telegram se ambíguo.

Durante o dia, o OpenClaw checa inboxes, aponta lacunas e prepara consolidação.

O que amadureceu vira memória oficial.

Time e agentes consultam antes de agir.


## A estratégia nasce no pessoal. O que pode operar vai para a empresa.

Sócios usam agente para brainstorm, conselho, conversas estratégicas e decisões. Mas nem tudo que nasce ali deve entrar no cérebro da empresa. O papel do diretor é filtrar.


### Ideias estratégicas

Você pensa no cérebro pessoal: tese de produto, posicionamento, campanha, GTM, parceria.


### Conselho e direção

Você registra discussões, premissas e decisões. Algumas viram operação; outras ficam privadas.


### /sync-empresa ou /sync-diretoria

O que pode ser visto pelo time vai via /sync-empresa . O que dispara os 3 gatilhos (sensível) vai via /sync-diretoria . Cada skill vive no repo correspondente.


### 3 gatilhos

Se envolve dinheiro nominal, pessoa específica ou jurídico, não vai para a empresa. Vai para diretoria.


## O cérebro da diretoria existe porque nem todo contexto da empresa é do time.

Esse é o gancho para a próxima aula. A empresa precisa de memória compartilhada, mas também precisa de fronteira. Diretoria nasce para proteger o sensível.


### Dinheiro com nome próprio

Salário, comissão, bônus individual, pró-labore, dívida nominal.


### Pessoa específica

Avaliação, feedback direto, conflito, contratação, desligamento.


### Peso contratual/jurídico

Contrato, NDA, litígio, compliance, LGPD, governança restrita.


### Resumo de roteamento

Operacional e compartilhável? Cérebro da empresa. Individual? Cérebro pessoal. Sensível? Cérebro da diretoria.


## Mostre duas pessoas colaborando antes da consolidação.

Aqui entra a demo ao vivo: setup da estação, setup do OpenClaw da empresa, duas capturas em inboxes diferentes, /sync-empresa para o inbox compartilhado, consulta provisória por outra pessoa e rotina de consolidação.

Co-work cria o cérebro da empresa a partir do template.

Configura o agente da empresa e a rotina de consolidação.

Diretor salva uma regra; colaborador salva uma evidência ou dúvida.

Ambos fazem /sync-empresa e conseguem consultar staging/inbox antes do canônico.

Contexto vai para area correta: vendas, marketing, suporte etc.

Outro membro consulta a memória sem pedir contexto ao founder.


## O “aha moment” é o time usando a mesma memória.

A validação da aula 2 não é recall individual. É colaboração: uma pessoa captura, outra consegue usar a captura sincronizada ao longo do dia, e depois o OpenClaw consolida sem depender do founder repetir tudo.


### O agente ficou operacional.

Ele não apenas “lembrou”. Ele transformou uma decisão solta em regra consultável por vendas, time e futuros agentes.

Métrica de validação: outra pessoa consegue agir melhor amanhã porque o contexto de hoje virou memória da empresa.


## Se você entendeu isso, a aula cumpriu o papel.

Antes de ir para a diretoria, você precisa conseguir responder estas perguntas sem decorar comando.

Um repo operacional compartilhado que guarda contexto, rotinas e skills da empresa.

Captura local, /sync-empresa para staging/inbox compartilhável, consulta provisória durante o dia e rotina do OpenClaw consolidando para main.

Pessoal conhece você. Empresa coordena o time e os agentes operacionais.

Porque existe contexto da empresa que não pode ser contexto do time.

Roda as rotinas da empresa: sync, consolidação, digest, cobrança, criação de skills e resposta com contexto permitido.

Brainstorm e estratégia no pessoal; distribuem ao time só o que é operacional e seguro.


## O que tá rodando debaixo do capô do cérebro da empresa.

Mesma lógica do cérebro pessoal — só que com mais gente envolvida, então a proteção importa ainda mais. São 2 mecanismos pequenos que evitam confusão grande.


### /cerebro

Aqui ele é obrigatório. Quando você abre o Claude na pasta da empresa, é a primeira coisa que roda. Em segundos, o agente sabe os 3 cérebros, sabe quem é você (sócio ou colaborador), sabe o que pode propagar pra onde. Sem isso, ele tenta adivinhar — e dá ruim.


### Agente não salva sozinho

Mesma trava do cérebro pessoal, mesma lógica: nada é salvo automaticamente . Só as skills oficiais ( /sync-empresa , rotinas como consolidar-estacoes ) destravam. O Léo, no servidor dele, tem a chave por configuração — então ele consolida à noite normalmente. Mas Claude na sessão de qualquer pessoa? Bloqueado por padrão.


## O cérebro da empresa tira a operação da cabeça do founder.

Ele cria uma memória comum para pessoas e agentes trabalharem melhor. O cérebro pessoal prova a portabilidade da memória. O cérebro da empresa prova a colaboração. A diretoria vem depois para proteger o que não pode ser coletivo.
