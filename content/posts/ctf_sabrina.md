+++
title = "[Memórias #1] CTF — Menina de Cybersec"
date = 2026-03-27
cover = "Devaneios---ctf.png"
images = ["Devaneios---ctf.png"]
+++

Entre os dias 11 e 15 de novembro de 2022, quando eu dava meus primeiros passos em segurança, participei do CTF da comunidade @meninadecybersec. Guardo com muito respeito esta memória, porque foi um divisor de águas no meu desenvolvimento.   

Faço questão de compartilhar o write-up original, sem edições, pois honro cada erro cometido; eles foram a base do meu aprendizado. Foi através dessa dedicação que conquistei uma bolsa integral no San Jose Institute of Technology (SJIT), expandindo ainda mais os meus horizontes na área.

---
## Introdução

Entre os dias 11 e 15 de Novembro, foi realizado um evento de CTF (Capture The Flag) no servidor oficial da comunidade @meninadecybersec no Discord.

Apesar do nome, o servidor criado pela @meninadecybersec/Sabrina Ramos é aberto a todos. A comunidade é conhecida por conter diversos recursos gratuitos, networking e eventos voltados aos iniciantes em cibersegurança.

Capture The Flag, como o nome já sugere, é uma competição lúdica na qual se testam os conhecimentos em segurança da informação em busca de “bandeiras”, que são a resposta dos desafios. Neste caso, foram postas à prova as habilidades em diversas categorias, incluindo Análise de Artefato, OSINT-GEOINT, Análise de Phishing e Programming.

---
## Preparação    
Após acessar o link disponibilizado no servidor, nos deparamos com a interface na qual estão os Challenges, desafios preparados especialmente para o evento, conforme abaixo. Apesar de não haver uma ordem exata para realização dos desafios, podemos iniciar pela categoria Easy, que contém challenges de nível fácil.  

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*AYrJu0e2vwUXDyBW"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Alguns dos challenges disponíveis na plataforma</em></p>
</div>
     
Todas as flags seguem o formato: MCS{solução_do_desafio}. MCS (Menina de CyberSec) é um prefixo obrigatório, já o conteúdo dentro das chaves é a resposta dos desafios, propriamente dita. Sabendo disso, vamos jogar!

---
## Desafio: Nomeie Essa Tool (1 a 3) — Easy   
Iniciamos com uma série de três desafios, que podem servir como ponto de partida para os demais. Ao abrir os desafios Nomeie essa Tool, são fornecidas algumas imagens, que podem ser muito familiares para estudantes e profissionais de segurança.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*tgzihCL_yBHRnw2qsB_31w.jpeg"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>1 — qual_o_nome_disso.jpg</em></p>
</div>

<div>
  <img src="https://miro.medium.com/v2/resize:fit:450/format:webp/0*G85IabpnwArqynLq"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>2 — o_que_e_isso_esta_vendo_o_meu_futuro.jpg</em></p>
</div>

Realizando uma busca reversa pelas imagens em qualquer mecanismo de pesquisa, como o famigerado Google Lens, é possível descobrir o nome das duas ferramentas, que se encaixam perfeitamente nas flags solicitadas.

Flag Desafio 1: MCS{burp_suite} — Ferramenta de pentest web.

Flag Desafio 2: MCS{nmap} — Ferramenta para port scan na rede.

O terceiro challenge da série, em especial, apresentou a seguinte imagem, com o nome de endianness.jpg.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*UxG7OJPS7rp2wc_B"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>endianness.jpg</em></p>
</div>

Em breve pesquisa pelo termo, notamos que o endianness se refere à forma como os bytes são organizados na memória do computador. Existem duas arquiteturas diferentes de armazenamento dos bytes:

-Little-Endian: Quando os bytes são armazenados do maior para o menor.

-Big-Endian: Quando os bytes são armazenados do menor para o maior.

Percebe-se que as setas estão apontando para a primeira sequência, que é crescente. Nesse caso, sabemos que estamos diante de um big-endian.

Flag Desafio 3: MCS{big_endian}

>Para aprender sobre Linguagem de Baixo Nível, Assembly, binários e engenharia reversa, o Instagram da @hacknlearn/
Carolina Trigo
 é um prato cheio!

---
## Desafio: Hackerman — Easy
Neste desafio, é fornecido apenas o arquivo gostariadesaberqualserie.jpg, que é auto explicativo. Ao abri-lo, vemos o seguinte.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*6438jR73VxIxzW2A"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>gostariadesaberqualserie.jpg</em></p>
</div>


Para aqueles que já acompanham filmes e séries de temática hacker, esse desafio é muito simples. Caso contrário, basta pesquisar o termo “Hackerman” na internet para obter um meme, baseado no personagem principal da série Mr. Robot (Elliot Alderson).

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*xEWTjES0kUQFr67y"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Hackerman! 😎</em></p>
</div>

Nota-se também, na primeira imagem, o termo “fsociety”, que refere-se ao nome do grupo hacker fictício da série, do qual o menino Elliot faz parte. Além disso, também há o link whoismrrobot.com, mostrado no navegador.

Flag: MCS{mr_robot}

---
## Desafio: O SOC Sofre… (1) — Phishing Analysis
>Qual endereço de IP enviou o e-mail?

O primeiro desafio de Análise de Phishing consiste em descobrir o IP de quem enviou um e-mail e, para tanto, é fornecido o arquivo de e-mail (.eml) a ser analisado.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*gqt63xNmyftb0uAs"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Arquivo .eml</em></p>
</div>

Neste caso, optamos por utilizar o Microsoft Outlook, em uma máquina com Windows, para abrir o arquivo e visualizar seu conteúdo. Claramente, uma tentativa de phishing contra o destinatário da mensagem.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*Oo0ZbMUkEJnDvgbp"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>E-mail aberto</em></p>
</div>

A princípio, o objetivo do desafio é localizar o IP do remetente, informação que pode ser encontrada no cabeçalho/header.

Selecionando a opção Arquivo, no menu superior, chegamos à página de Informações, que mostra algumas das informações da mensagem e permite, inclusive, ler suas propriedades e opções avançadas.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*EBMMJtOJpi3_Qh94"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Informações do E-mail</em></p>
</div>

Clicando em Propriedades, chegamos a uma janela crucial do challenge.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*daa1PJtPtX4LFdPP"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Propriedades do E-mail</em></p>
</div>

A informação que procuramos se encontra no header do e-mail, porém sua leitura completa pode ser exaustiva. Felizmente, existem diversas ferramentas para análise de header, dentre elas o MxToolBox.

Ao colar o conteúdo completo do cabeçalho no MxToolBox, chegamos ao seguinte resultado e podemos descobrir qual é o IP do remetente, obtendo assim a flag do desafio.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*lVsHgEufX0A-QbSG"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Informações extraídas do header — 1</em></p>
</div>

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*0mkcrtqPu1ueLbrW"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Informações extraídas do Header — 2</em></p>
</div>

Flag: MCS{209.85.222.173}

---
## Desafio: O SOC Sofre… (2) — Phishing Analysis
>Qual e-mail preenche o campo ‘From:’?

Ainda na ferramenta MxToolBox, é possível verificar que, apesar de parecer ter sido enviado de uma fonte legítima, o adversário tenta se passar pelo banco da vítima para capturar suas informações.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*WW-BU26OGw3eV6gm"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Campo From, obtido pelo MxToolBox</em></p>
</div>

>From: “[Pontos ltauCartoes2.0 Liberados][048582186378611072]” <santormcconnellw9660@gmail.com>

Com um olhar um pouco mais atento ao endereço de email do remetente, a vítima pode evitar cair em um golpe e, claro, podemos obter nossa flag.

Flag: MCS{santormcconnellw9660@gmail.com}

---
## Desafio: O SOC Sofre… (2) — Phishing Analysis
>Quem foi a vítima desse e-mail?

Logicamente, a vítima é o destinatário do e-mail, aquela que recebeu o conteúdo malicioso em sua Caixa de Entrada. A resposta do desafio está nos campos “To” ou “Para”, assim como o corpo do email.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*lMbRdKjob3iHaTi1"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Corpo do E-mail</em></p>
</div>

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*fPCn5BEEuzsyBGtz"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Campo To, obtido através do MxToolBox</em></p>
</div>

Flag: MCS{rosinha@hotmail.com}

---
## Desafio: Fibowhat — Programming
Neste desafio, é fornecido um arquivo sem extensão, de nome fibonacci. Quando o abrimos — através de qualquer leitor de texto, podemos descobrir o objetivo do desafio, através da mensagem que consta no comentário da primeira linha:

> O que você imagina que tem de errado nesse código? O Erro é a flag, boa sorte =D

Também podemos visualizar um código desenvolvido na linguagem C, ficando claro que deve ser feito um review para descobrir qual é o erro.


<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*jRlxGCcIAKW3x-sM"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Leitura do arquivo com o comando cat, no Linux</em></p>
</div>

Em breve análise do código, verificamos que sua função principal não está presente. A função main, que é o ponto de partida dos códigos na linguagem C, não consta no arquivo.

Para funcionar normalmente, a linha 5 do código deve ser: int main().

Flag: MCS{main}

## Desafio: Keep calm, don’t panic — Programming
Abrindo o arquivo dontpanic.txt, fornecido neste challenge, obtemos o retorno abaixo.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/0*QMUuVOcdojLtFUWh"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Leitura do arquivo dontpanic.txt, novamente com o comando cat</em></p>
</div>

Com base nas informações contidas no arquivo, verificamos que Urban Müller criou, em 1993, a linguagem de programação esotérica chamada de Brainf**k. Sendo assim, executamos os caracteres do arquivo em um interpretador online de Brainf**k, obtendo como saída um simples “Hello world!”, que também é a flag do desafio.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/0*5i0z7F5uBBR3eRzo"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Conversão do código através de ferramenta online</em></p>
</div>

Flag: MCS{hello_world}

---
## Desafio: Onde está o Olly? Não! — OSINT-GEOINT
O primeiro desafio de OSINT-GEOINT é bastante curioso. O challenge fornece um arquivo de texto com as informações básicas para prosseguir com os demais da categoria, conforme abaixo.


<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*30QuDWHkeTtPjNk7EaAFZg.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Leitura do arquivo soconfia.txt, utilizando o Vim</em></p>
</div>

>Seu objetivo é descobrir qual é o aeroporto (sigla) e o país.
Dica: os destaques estão ali por um motivo!

Neste ponto, já obtivemos o perfil a ser analisado. O perfil @anna_serrana pode ser encontrado no Instagram — visto que é a principal rede social, quando se fala em post de fotos. Nele, foram publicadas diversas imagens que serão analisadas nos seus respectivos desafios.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*ZjTzuue44vCvKhYdxH7ZEQ.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Perfil @anna_serranna, no Instagram</em></p>
</div>

A primeira foto publicada no perfil mostra uma área similar a um terminal de embarque. A julgar pelo tamanho da estrutura e pela descrição da foto publicada, sabemos que se trata de um aeroporto.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*djgrbYvrWQdGqC4jB-CRPw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Primeira publicação de anna_serranna</em></p>
</div>

>quem vê o close não vê o corre   
Eu amo este aeroporto ❤️   
🚩o Olly está por aqui?

Além da imagem acima, também há outro recurso que pode ser utilizado para descobrir de qual aeroporto se trata: a imagem na aba de Destaques.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*8nrPXizaQyIxS5gr1mYmoQ.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Imagem das filas de embarque do aeroporto</em></p>
</div>

Novamente, através de pesquisa reversa com o Lens, pudemos localizar o local exato onde a foto foi tirada, o Aeroporto de Istambul (cuja sigla é IST), localizado na Turquia.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*tcjOvJETVYPwPIbYuZvqFw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Resultado da busca com o Google Lens</em></p>
</div>

Vale lembrar que podem ser usados mecanismos de busca diferentes e diversas fontes na internet, que chegariam ao mesmo resultado.

Flag: MCS{ist_turquia}

---
## Desafio: Stalker on maps parte 1 — OSINT-GEOINT
O objetivo deste desafio, segundo o arquivo .txt fornecido, é analisar o perfil @anna_serranna mais uma vez, a fim de montar uma linha geográfica de suas viagens.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*seRVrj0TvckCyshW6MfXEw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Leitura do arquivo fornecido maps.txt</em></p>
</div>

A próxima foto publicada no perfil mostra uma rodovia, com placas indicando duas localidades, sendo elas Amarillo (Texas), e Ft. Smith (Arkansas). Estando ambos os locais nos Estados Unidos (o que também poderia ser deduzido pela publicação com a foto do hamburger americano), limita-se o escopo das buscas.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*AOEYoJFAfzBzvglFEK43Ww.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Segunda imagem publicada no Instagram</em></p>
</div>

Sabe-se que e estrada da imagem é a I-40, dada a indicação das placas, então o que buscamos é uma localização, na referida estrada, que esteja próxima aos dois locais.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*eiZ3SVpcJ_ZGSHZYSIMENQ.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Caminho traçado entre Amarillo e Ft. Smith pela estrada Interestadual 40</em></p>
</div>

Percebe-se, segundo essa lógica, que o local central entre as duas localidades indicadas nas placas, está no estado de Oklahoma. Da mesma forma, buscando por informações das saídas 120A e 120B (indicadas nas placas), verifica-se que ambas estão no estado de Oklahoma.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:556/format:webp/1*VzWjNPcVj3207BqV0uA03g.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Informações da EXIT 120A</em></p>
</div>

Touché! Descoberta a flag do desafio.

Flag: MCS{oklahoma_estados_unidos}

## Desafio: Stalker on maps parte 2— OSINT-GEOINT
Assim como o desafio anterior, o desafio Stalker on maps — parte 2, solicita uma localização no mapa, com a diferença de que são encontradas três imagens diferentes do mesmo local no perfil da @anna_serranna, sendo a terceira imagem, talvez, a mais significativa.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*msCbxnh1FnZe5RuNStVKGA.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Imagem 1 — Placa indicativa</em></p>
</div>
   

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*RBkbuV93C0EGxsCPEG46mw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Imagem 2 — Tráfego de veículos</em></p>
</div>
   

<div>
  <img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*APLeydDA1QmVO5dF5sPU-Q.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Imagem 3 — Indicações de local nas placas</em></p>
</div>
   

Com base nas imagens fornecidas, temos a certeza de que o lugar onde Anna passou tem o Espanhol como língua oficial e está próximo a uma saída de caminhões. Apesar da dificuldade na leitura, é possível perceber os seguintes dizeres na placa (imagem 3): San Juan, Santurce e Hato Rey. Pesquisando por qualquer um dos termos, chegamos à informação de que o país que abriga esses locais é Porto Rico/Puerto Rico.

Além disso, podemos averiguar que Santurce e Hato Rey são dois bairros importantes de San Juan, mas essas informações não seriam suficientes para achar o local exato da imagem.

Buscando por “San Juan Puerto Rico Camiones” no Google Maps, podemos verificar a existência de diversas companhias de transporte em San Juan, concentradas em uma região específica do país, limitando o range das buscas.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*A8ENnOyT_OdZTirBGF2-Mw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Companhias de transporte e caminhões no norte de San Juan, Porto Rico</em></p>
</div>

Observando as ruas nas proximidades, chegamos próximos à Ecw San Juan, que possui uma garagem de caminhões, sendo a mesma da imagem e podendo ser vista a partir da rodovia Expreso John F. Kennedy.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*NVp0Jto89FtZQrPq5Hj_3A.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"></p>
</div>

Comprovamos, assim, que o local onde a foto foi tirada é em San Juan.

Flag: MCS{sanjuan_porto_rico}

---
## Desafio: “Me manda no e-mail” — Análise de Artefato
O primeiro dos desafios de Análise de Artefato fornece um arquivo .pdf para análise e solicita algumas informações do mesmo. A fim de não comprometer a máquina, o arquivo foi analisado através de uma máquina virtual (VM) com o Kali Linux instalado.

>Qual o SHA-256 desse artefato?

Com o arquivo baixado na máquina (sem a necessidade de abrí-lo), podemos utilizar o comando sha256sum para extrair o hash em SHA-256 do arquivo e completar o desafio rapidamente.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*JnbaqRFSxiP95jSuSzTxuw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Uso do comando sha256sum para obter o hash do arquivo pdf</em></p>
</div>

Flag: MCS{6a4440a995dd031554d6f3ff71f196896287c20f5c6e664b85876b9adc6058c4}

---
## Desafio: Tem técnica, mas não tem tática… — Análise de Artefato
O desafio é uma sequência do anterior e tem o mesmo arquivo como base.

>Em qual técnica do Mitre Att&CK esse artefato se encaixa?
Desafio: Cuidado com a pesca!

Primeiramente, o que sabemos sobre o arquivo?

Sabemos que o arquivo em .pdf teria sido enviado, supostamente, pela Caixa Econômica Federal. Porém, ao analisá-lo, verificamos que bastaria apenas um clique em qualquer parte do documento para que a vítima fosse direcionada a um site malicioso, possivelmente para captura de informações.
Press enter or click to view image in full size

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*wgSlJy34fT5BZ8tLepjbSQ.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"></p>
</div>

Para responder ao desafio, seria preciso acessar o Mitre Att&CK, uma ferramenta online que funciona como uma base de conhecimento das táticas e técnicas usadas por atacantes no mundo real.

>Desafio: Cuidado com a pesca!

Com base na dica fornecida, sabemos que é uma técnica de phishing (pesca em inglês), método de ataque bastante comum. Vejamos um pequeno resumo sobre o phishing e como se dá o ataque, segundo o próprio Mitre.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*uNlUML0cSK4ONnoIIBvzwQ.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Página com informações sobre Phishing no Mitre Att&CK</em></p>
</div>

>“Os adversários podem enviar e-mails às vítimas contendo anexos ou links maliciosos, normalmente para executar código malicioso nos sistemas das vítimas (…). O phishing também pode envolver técnicas de engenharia social, como se passar por uma fonte confiável.

Como visto na imagem, o phishing possui três sub-técnicas. Após leitura e baseado na própria descrição da técnica T1566.002, percebemos que é a que mais se aproxima da técnica usada pelo adversário.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*cMTueFZRxta4VUDo0ZuKdg.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Parte da descrição sobre Spearphishing Link no Mitre Att&CK</em></p>
</div>


>“Geralmente, os links serão acompanhados por um texto de engenharia social e exigem que o usuário clique ativamente ou copie e cole um URL em um navegador, aproveitando a user execution.”

Temos aqui a descrição perfeita da técnica utilizada pelo atacante, sendo a instituição bancária usada para a engenharia social.

Flag: MCS{spearphishing_link}

---
## Desafio: Não sei, Berg, tá estranho… — Análise de Artefato
>Algum security vendor sinalizou esse artefato como malicioso?

Existem diversas plataformas para análise e sandbox de malwares, incluindo ferramentas gratuitas online. Por familiaridade, utilizamos o Hibrid Analysis.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*K6UKYrjVCiLNlkYdTwbZyw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Tela inicial do Hibrid Analysis</em></p>
</div>

Basta fazer o upload do arquivo no sistema para obter como retorno diversas informações interessantes e úteis para a análise.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*mo5qXn3h8Lbf3tbmunt0Tg.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Análise do arquivo do desafio após upload no site</em></p>
</div>

O sistema já demonstra que o arquivo é malicioso, com pontuação de ameaça de 95/100, além de dar informações relevantes como o SHA256, solicitado em desafios anteriores.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*_Y1r0i2Tk4CJ2NdHI6SPvg.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Detecção de técnicas do Mitre Att&CK, segundo o Hibrid Analysis</em></p>
</div>

Após upload do arquivo no site VirusTotal, podemos verificar que o Security Vendor ESET-NOD32 já havia reportado o arquivo e o sinalizado como malicioso.

<div>
  <img src="https://miro.medium.com/v2/resize:fit:720/format:webp/1*0HqtDWd54deWElTfeuOkHw.png"
       style="display: block; margin: 0 auto;">
  <p style="text-align: center;"><em>Tela inicial do Hibrid Analysis</em></p>
</div>

Conclui-se que, somente com o Hibrid Analysis, pode ser concluída boa parte dos desafios desta categoria, mas é sempre importante utilizar mais de uma tool, antes de chegar a qualquer conclusão sobre o artefato.

Flag: MCS{eset_nod32}

---
## Disclaimer e Encerramento
Impossível deixar de agradecer às amigas, idealizadoras dos desafios e moderadoras do servidor, por sempre nos proporcionarem conhecimento de forma acessível e manterem uma comunidade fantástica, com mais de 2 mil pessoas, unidas no objetivo de fortalecer a Segurança Cibernética no Brasil.
   
Sabrina Ramos - Luana Vieira - Carolina Trigo - Lais Camargo

Vocês são demais! ❤

Foram omitidos deste write-up os seguintes desafios:

Easy — Fã número 1 da menina de CyberSec, Network — Programming, Forense — Phished Accounts, Web — Não odeio o Javascript & Nosferatu.

---
Muito obrigado pela leitura! Nos vemos na web!