+++
title = "RFC 4120 - Tickets para o Inferno"
date = 2026-09-15
cover = "kerberos.png"
images = ["kerberos.png"]
+++

Em fevereiro de 1988, o MIT publicou um pequeno diálogo sobre um problema que mal havia nascido e já começava a assombrar quem estava construindo redes: como autenticar alguém em uma rede sem precisar confiar em cada computador que participa dela?

O texto é fictício. Dois personagens, Athena e Eurípides, começam tentando resolver um problema aparentemente simples. Eles precisam de uma forma de autenticar usuários em uma rede aberta. A cada solução, porém, aparece um novo problema. Eles corrigem uma coisa, quebram outra, voltam à prancheta e continuam.

No fim, Athena decide que o melhor nome é o do cão de três cabeças que guarda a entrada do Hades: Kerberos.

A brincadeira funciona até tecnicamente. Kerberos é a grafia grega de Κέρβερος, o nome do cão que os romanos chamaram de Cerberus. E, curiosamente, o diálogo fictício publicado pelo MIT em 1988 descreve um sistema bastante parecido com o Kerberos que havia sido desenvolvido no próprio Projeto Athena.

Permita o querido leitor que eu o conduza, porque gosto muito dessa história, que já começa no lugar certo, ou seja, no problema.

É muito fácil olhar para a tecnologia que existe hoje e imaginar que ela sempre esteve ali. Login, senha, domínio, compartilhamento de arquivos, acesso remoto, autenticação. Coisas tão comuns que quase passam despercebidas (e na verdade, este é o intuito).

Grande parte da computação moderna, porém, nasceu quando essas coisas ainda precisavam ser inventadas, e os problemas eram muito mais concretos do que os nomes que demos a eles depois.

O Kerberos nasce, então, dentro deste contexto.

---

# O problema de Athena

Em 1983, o MIT iniciou o Projeto Athena, um grande esforço de computação distribuída feito em parceria com a Digital Equipment Corporation e a IBM. A proposta era espalhar computadores pelo campus e permitir que estudantes, professores e pesquisadores utilizassem uma infraestrutura compartilhada de computação e serviços.

A ideia parecia promissora, mas trazia consigo um problema bastante desagradável, já que os computadores não eram necessariamente confiáveis.

Uma máquina usada por estudantes poderia ser alterada. Um programa poderia ser modificado. Um atacante poderia controlar um computador da rede. Alguém poderia observar o tráfego passando por ela.

Então imagine, querido leitor, que eu esteja sentado diante de um computador e digito:

`rodrigo`

O computador responde:

`Olá, Rodrigo.`

Excelente. Temos um problema.

**Quem disse que aquele computador deveria acreditar em mim?**

Se a máquina estiver comprometida, ela pode aceitar qualquer nome. Pode também capturar a senha que eu digito e entregá-la a outra pessoa.

O problema fica mais interessante quando percebemos que o computador onde eu estou sentado também pode ser parte do problema.

A rede precisa de uma forma de autenticação que não dependa da palavra do próprio computador.

Em 1985, David Clark supervisionou no MIT duas teses de bacharelado diretamente ligadas a esse problema. Eric Jaeger trabalhou em um protocolo de controle de acesso baseado em uma terceira parte confiável. Clifford Neuman desenvolveu o Sentry, acrescentando mecanismos de controle de acesso e contabilidade, além de implementar um servidor protótipo.

Depois de concluir sua tese, Neuman passou a trabalhar com Steve Miller no Projeto Athena, e desse trabalho surgiu o Kerberos.

A primeira implementação foi concluída em 1986 e entrou em produção no mesmo ano. Em janeiro de 1987, o Kerberos já era o único mecanismo de autenticação do Project Athena, atendendo 5.000 usuários, 650 computadores e 65 servidores.

É uma história curiosa, o Kerberos é o que muitos chamariam de “case de sucesso”. Afinal, quem diria que uma tecnologia que hoje está em todo lugar (digo sem medo de errar), surgiria através de um grupo de estudantes universitários, que sempre são tão desacreditados? 

---

# Um triângulo amoroso

A ideia fundamental do Kerberos pode ser resumida de maneira quase indecente de tão simples.

Imagine que eu queira entrar em uma festa. Eu chego à porta e digo:

"Sou Rodrigo."

O segurança olha para mim.

"Prove."

Eu poderia apresentar algum documento. O segurança poderia conhecer minha assinatura. Poderia ainda perguntar alguma coisa que apenas Rodrigo saberia, mas suponhamos que eu não confie naquele segurança. Ou melhor: suponhamos que NINGUÉM confie nos seguranças espalhados pela cidade inteira. A solução pode ser colocar uma autoridade no meio.

Eu me identifico diante de uma entidade central em quem todos confiam. Essa entidade confirma quem eu sou e me entrega uma credencial. Quando eu quiser entrar em outra festa, apresento a credencial.

O segurança não precisa conhecer minha senha, e eu tambm não preciso confiar nele. Nós dois confiamos em uma terceira parte. Essa é a ideia central do Kerberos: uma **terceira parte confiável**.

O protocolo foi inspirado no trabalho de Needham e Schroeder sobre autenticação em grandes redes, além de modificações posteriores feitas por Denning e Sacco. A ideia era utilizar uma autoridade central capaz de distribuir credenciais e chaves de sessão para entidades que precisassem se comunicar.

Essa autoridade é o KDC (**Key Distribution Center).** Em bom português**:** Centro de Distribuição de Chaves, embora perca todo o seu glamour, então vamos usar somente KDC.

No Kerberos moderno, o KDC fornece dois serviços lógicos: o Authentication Server, ou AS, responsável pela autenticação inicial e emissão de TGTs, e o Ticket-Granting Server, ou TGS, responsável por emitir tickets para serviços específicos.

Agora temos quase tudo de que precisamos. Ou quase, porque ainda falta uma coisa: o ticket.

---

# O ingresso para o Hades

O ticket é uma credencial emitida pelo KDC que permite ao cliente provar sua autorização para acessar determinado serviço.

Façamos aqui uma distinção importante. O ticket **não é simplesmente um papel digital dizendo "esse usuário é Rodrigo", e**le contém informações destinadas ao serviço e é protegido criptograficamente com uma chave que o próprio serviço conhece.

Isso permite uma ideia bastante chique:

O cliente recebe o ticket, mas não precisa conseguir modificá-lo.

O servidor recebe o ticket, consegue verificá-lo, e não precisa conhecer a senha do usuário.

O KDC consegue emitir essas credenciais porque conhece as chaves secretas envolvidas.

A partir daí, podemos acompanhar uma autenticação inteira.

Agora, vamos imaginar que eu esteja em uma máquina do domínio e queira acessar um serviço chamado:

`files.exemplo.local`

Eu não quero digitar minha senha para o servidor de arquivos (até porque ele pode não ser um) e o servidor de arquivos também não precisa conhecer minha senha, então a conversa começa em outro lugar.

---

# Primeiro: quem é você?

O cliente procura o Authentication Server e envia uma requisição inicial. Em termos simplificados, a mensagem diz:

> "Eu sou Rodrigo. Preciso de credenciais para usar a rede."
> 

O AS consulta sua base de dados e encontra a conta correspondente. Ele conhece a chave longa associada àquela identidade, normalmente derivada da senha do usuário. Essa chave é usada para proteger determinados dados que só o cliente que conhece a credencial correta deveria conseguir recuperar.

O AS então produz duas coisas importantes: A primeira é uma **chave de sessão**. A segunda é um **Ticket-Granting Ticket**, o famoso TGT.

O TGT é criptografado com uma chave secreta do serviço de concessão de tickets. O cliente pode armazená-lo e carregá-lo consigo, mas não precisa ler seu conteúdo para utilizá-lo.

A ideia é bastante bonita. Pense da seguinte forma: O cliente recebe uma credencial que pode apresentar posteriormente sem precisar entregar sua senha a cada serviço. Ufa!

É por isso que o Kerberos permite algo que hoje parece trivial: **Single Sign-On.**

Uma autenticação inicial pode produzir credenciais reutilizáveis durante um período determinado, permitindo acessar vários serviços sem repetir o processo inteiro.

No Kerberos V5, a autenticação inicial e suas proteções podem envolver mecanismos de pre-authentication, e os detalhes dessa primeira troca são mais sofisticados do que essa pequena história deixa parecer. A própria RFC 4120 trata a autenticação inicial como parte de um protocolo maior, no qual a senha do usuário não precisa ser enviada em claro pela rede.

O que interessa guardar agora é apenas isto: **eu tenho um TGT.**

E ainda não falei com o servidor de arquivos.

---

# Segundo: o que você quer?

Agora eu quero acessar `files.exemplo.local`.

Poderia simplesmente mandar meu TGT para o servidor, só existe um pequeno probleminha. O TGT não foi emitido para `files.exemplo.local`, ele é uma credencial para conversar com o serviço de concessão de tickets.

Então o cliente vai até o TGS e diz:

> "Aqui está meu TGT. Quero um ticket para o serviço `files.exemplo.local`."
> 

O TGS verifica o TGT. Se tudo estiver correto, ele emite um novo ticket destinado especificamente ao serviço solicitado. Esse é o **service ticket**.

Mais uma vez, o cliente recebe também uma chave de sessão associada àquele relacionamento.

Agora temos algo muito interessante: Existe um ticket para falar com o TGS. Existe outro ticket para falar com o serviço. E cada peça tem uma função diferente.

O TGT diz, em essência:

> "Este cliente já foi autenticado e pode pedir credenciais para outros serviços."
> 

O service ticket diz:

> "Este cliente pode utilizar este serviço."
> 

E ainda existe uma última pergunta.

Como o servidor sabe que a pessoa apresentando o ticket é REALMENTE quem recebeu aquele ticket?

---

# Terceiro: prove que é você

O cliente finalmente chega ao servidor. Apresenta o service ticket. O servidor consegue decifrar o ticket porque possui a chave secreta correspondente, mas ainda existe uma preocupação: Se alguém capturar esse ticket na rede, poderia tentar reapresentá-lo.

É aqui que entra o **authenticator**. O cliente envia, junto do ticket, informações adicionais protegidas com a chave de sessão. Entre elas existe um timestamp. A função disso é demonstrar que quem está apresentando o ticket possui a chave de sessão correspondente e que aquela apresentação aconteceu dentro de uma janela de tempo aceitável.

O servidor verifica o ticket. Verifica o authenticator. Verifica o timestamp. E, se tudo estiver correto, aceita a autenticação.

A RFC 4120 explica essa preocupação: um ticket interceptado pode ser repetido, então informações adicionais, protegidas pela chave de sessão e contendo um timestamp, servem para demonstrar que a requisição foi produzida recentemente por quem possui aquela chave.

É aqui que uma pequena preocupação começa a aparecer: o tempo (do qual falei em texto recente).

---

# O preço de confiar no tempo

Se o protocolo depende de timestamps, os computadores precisam ter seus relógios razoavelmente sincronizados. Se a máquina do cliente acredita que são 14h05, mas o servidor acredita que são 14h42, a definição de "recente" começa a ficar um pouco complicada.

O Kerberos, portanto, resolve um problema e traz algumas exigências junto.

1. Você precisa de um KDC confiável.
2. Precisa proteger as chaves secretas.
3. Precisa manter os relógios dos computadores suficientemente sincronizados.
4. Precisa definir tempos de validade.
5. E precisa proteger uma estrutura cuja autoridade alcança vários serviços.

Essa é uma das partes que acho mais interessantes no Kerberos. Ele concentra a confiança. Em uma rede sem Kerberos, várias máquinas poderiam tomar suas próprias decisões sobre quem é confiável. Com Kerberos, todos passam a depender de uma autoridade comum, e isso simplifica muita coisa.

Por outro lado, cria um ponto crítico que você, querido leitor, inteligente como é, já percebeu: Se o KDC for comprometido, o problema deixa de ser local e passa a ser estrutural. Imagine o estrago disso em um ambiente Windows real, como estamos acostumados.

---

# Cão de guarda do domínio

Décadas depois do Projeto Athena, a ideia continuou viva.

Kerberos se tornou parte fundamental do Active Directory Domain Services, no qual o KDC é implementado como um serviço de domínio e utiliza o Active Directory como sua base de contas. Em ambientes Windows, o KDC continua oferecendo os dois papéis que vimos aqui: Authentication Service e Ticket-Granting Service.

A escala mudou, e a universidade virou empresa, os estudantes viraram funcionários, os servidores cresceram, o compartilhamento de arquivos virou centenas de aplicações, bancos de dados, serviços internos, etc., etc., etc.

A ideia central, porém, continuou muito parecida.

1. Você entra no domínio.
2. Recebe um TGT.
3. Solicita tickets para os serviços.
4. Apresenta esses tickets.
5. E o servidor verifica as credenciais sem precisar receber sua senha.

Quando você trabalha com segurança ofensiva, esse mecanismo começa a ficar ainda mais interessante, porque uma estrutura construída ao redor de tickets também significa que existem tickets que podem ser roubados, reutilizados, forjados ou explorados quando alguma das chaves fundamentais é comprometida.

Daí surgem nomes que já assustaram muita gente em um laboratório de Active Directory:

**Kerberoasting, Pass-the-Ticket, Golden Ticket**, e por aí vai…

Eles são assuntos muito maiores que este texto e merecem seus próprios capítulos. O importante aqui é perceber de onde essas técnicas vêm. Elas são consequências de uma arquitetura baseada em uma cadeia de confiança.

---

# Do pouco ao muito

Agora, veja que ironia: Quando o Projeto Athena começou, a preocupação era bastante específica: como fazer um campus universitário funcionar como uma grande rede distribuída?

A resposta acabou atravessando décadas de computação. O próprio MIT registra que tecnologias surgidas no Projeto Athena, entre elas o Kerberos e o X Window System, ultrapassaram o ambiente universitário e se tornaram importantes para a computação distribuída em escala muito maior.

Esse talvez seja o maior motivo pelo qual eu quis trazer esse assunto, porque entendo que existe uma péssima tendência no mercado atualmente: Nós só enxergamos as empresas.

Microsoft. Google. Amazon. Apple.

Enxergamos datacenters, laboratórios bilionários, produtos globais e sistemas que parecem grandes demais para terem começado como qualquer outra coisa.

Só que, quando voltamos algumas décadas, encontramos algo menos impressionante à primeira vista: Uma faculdade, um problema, algumas pessoas, uma ideia, um protótipo e um grupo de doidinhos querendo colocar seus planos em prática.

É fácil olhar para isso e imaginar uma linha reta entre o laboratório e o produto, mas a história sempre é tortuosa. Houve erros, revisões, vulnerabilidades, mudanças de protocolo e novas exigências. O próprio Kerberos mudou de versão e continuou sendo estudado, criticado e revisado por décadas. A RFC 4120, por exemplo, descreve o Kerberos V5, evolução da versão anterior, e registra parte desse caminho.

O ponto central que trago é que tecnologia, em qualquer sentido da palavra, nasce quando alguém está tão incomodado com um problema a ponto de passar algumas madrugadas tentando fazer aquilo funcionar.

No caso do Kerberos, esse incômodo começou com uma pergunta relacionada a segurança e confiança: **como saber quem está do outro lado da rede?**

O bom é que agora, ninguém precisará responder, basta apresentar seu ticket! Afinal, se existe um lugar onde ninguém deveria entrar sem autorização, é o inferno corporativo.

Muito obrigado pela leitura até aqui, querido leitor.