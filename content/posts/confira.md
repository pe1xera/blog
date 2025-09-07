+++
title = "доверяй, но проверяй"
date = 2025-09-06
cover = "confira.png"
images = ["confira.png"]
+++

“Confie, mas confira” — um ditado russo que deveria ser mantra para qualquer brasileiro que ousa abrir um aplicativo de banco sem tremores na mão. Agosto terminou com R$ 710 milhões desviados de contas que, em teoria, deveriam ser seguras. Setembro mal começou e já surgem notícias de prejuízos de R$ 3 milhões em golpes que, do lado de fora, parecem até filme de cinema, mas que, por trás das telas, seguem a exploração de vulnerabilidades e (possivelmente) scripts de engenharia social.

Não se trata apenas do crime organizado tentando faturar. É o sistema financeiro de uma nação inteira sendo testado, sistema esse que foi projetado para ser uma muralha de confiança entre seu dinheiro e terceiros. Acontece que entre declarações de políticos internacionais, movimentações suspeitas em fintechs e a evidente sofisticação de grupos criminosos, o cenário parece cada vez mais com o de Gotham City, mas sem um Batman.

Meu objetivo aqui não é dramatizar simplesmente por dramatizar. Trago o assunto porque é preciso entender o que acontece quando a segurança bancária se torna palco de guerra, quando aquilo que o povo sequer sabe como funciona é "cutucado", nos bastidores.

---

# Com vocês, o Pix!

Em um artigo recente, Rafael Miguel, que é líder de um time de engenheiros de software focados em cobranças financeiras, descreveu as mudanças que o Pix trouxe para o sistema financeiro brasileiro. Mas se você acha que é só clicar e pagar mais rápido, querido leitor, está bastante enganado. Cada transação que você faz é considerada uma mensagem única, percorrendo uma infraestrutura nacional que nunca dorme, gerida pelo SPI (Sistema de Pagamentos Instantâneos), do Banco Central, com responsabilidade que é até difícil de mensurar.

Funciona da seguinte forma: Quando alguém inicia um pagamento, o banco do pagador não conversa diretamente com o banco do recebedor. Ele empacota a ordem em uma mensagem criptografada e joga no SPI. O SPI valida, roteia, entrega, e o banco de destino processa a operação em milissegundos, devolvendo uma confirmação que retorna ao emissor. Por contrato, tudo deve acontecer em até 10 segundos. Loucura, né? Isso significa que existe um perigo real de dinheiro “no limbo”, em caso de falhas.

Rafael argumenta que o Pix, em essência, é um problema de consistência distribuída, ou seja, ele quer dizer que o Pix precisa garantir que o dinheiro desapareça de uma conta e apareça em outra de forma extremamente rápida. São sistemas diferentes, falando entre si, lidando com eventos em tempo real, tolerantes a falhas, idempotentes e cronometrados com precisão, algo que tem uma complexidade enorme.

A ordem de pagamento só é gerada, de fato, quando o usuário digita uma Chave Pix — CPF, e-mail, celular, etc. — que é resolvida pelo DICT, o diretório centralizado do Banco Central. O sistema responde quem é o dono da conta, o backend mostra a confirmação, o usuário aprova, e só então a transação é criada. Cada passo é minucioso, cada mensagem crítica, e qualquer erro nesse fluxo pode ser explorado.

---

# O Brasil em evidência

As notícias falam por si. Nas últimas semanas, várias instituições financeiras foram atacadas. Um caso notável envolveu a C&M Software, que integra vários bancos ao Banco Central. Credenciais foram comprometidas, permitindo que ordens válidas fossem enviadas ao sistema central. O Banco Central só identificou o problema ao perceber transações incomuns e bloqueou a integração da C&M para evitar propagação.  

Antes mesmo de entendermos como o ataque se deu, a Sinqia (que faz a ponte entre instituições financeiras e o Banco Central), sofreu um ataque que resultou em desvios estimados em centenas de milhões de reais, embora medidas emergenciais tenham limitado o impacto.  

Esses episódios mostram que a confiança formal, nos certificados, protocolos e assinaturas,  funciona sim, mas só até o ponto em que alguém consegue manipular processos internos. Não defendo o antropocentrismo, mas, no fim, voltamos mais uma vez ao fator humano, o chamado "elo mais fraco".  

Curioso notar que esses ataques coincidem com episódios recentes que poderiam desestabilizar a confiança no sistema: declarações internacionais desmerecendo o Pix e movimentações financeiras suspeitas envolvendo grupos organizados. Como sempre, o perigo surge na interseção entre tecnologia, confiança e comportamento humano.

O que vimos recentemente não é coincidência. É um teste de estresse real, expondo vulnerabilidades que muitas vezes são invisíveis até que alguém decida explorá-las. E, por trás da cortina, atores bem treinados sabem exatamente onde apertar os pontos frágeis.

---

# O preço da liberdade

Faz tempo que não abordo temas mais técnicos por aqui, mas não dá para ignorar quando a infraestrutura financeira do país, da qual todos dependemos, é posta à prova. Hoje, o Banco Central emitiu um alerta sobre um novo ataque hacker a uma instituição de pagamento, mostrando que essa novela mexicana ainda está longe de terminar.   

Só com a divulgação clara dos relatórios de invasões anteriores e, consequentemente, com a participação ativa da comunidade de segurança brasileira (que tem total capacidade de trabalhar nisso), o problema poderá ser contido e caminhar rumo a soluções efetivas.   

Transparência e colaboração, valores que nunca podemos abandonar - mesmo diante da calamidade.

Agradeço por sua leitura (e confiança) até aqui, querido leitor!