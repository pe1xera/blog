+++
title = 'Entendendo o ataque DDoS e seus impactos de uma forma simples'
date = 2023-01-17
cover = "ddos_capa.png"
+++

# #Introdução
Como parte do desafio de 30 dias de Cybersecurity (#30daysofcybersecurity) do servidor @MeninaDeCybersec, em seu 14º dia, fomos desafiados a postar um resumo sobre um ataque DDoS. Vejamos a descrição do challenge:

>_Pesquise sobre um ataque DDoS, veja como é possível identificá-lo e como mitigar (pelo menos uma forma de mitigação). Poste um resumo do que você pesquisou aqui, pode ser curiosidade, sua opinião etc, mas POSTE! Não precisa ser a análise mais completa de todas, lembre-se: você está estudando._

Tendo isso em mente, vejamos de forma simplicada como funciona esse tipo de ataque, possíveis formas de prevenção, assim como métodos de mitigação do mesmo.

>_Todas as imagens deste artigo foram geradas utilizando um pouco de imaginação e a Midjourney AI._
___
# #Conceitos-chave
{{< image src="../../../blog/static/ddos1.png" position="center" style="border-radius: 8px;" >}}

Para entender um DDoS, primeiro é necessário entender dois conceitos-chave, que estão diretamente relacionados ao tema. Vejamos alguns deles de forma simplificada e com exemplos didáticos fora da tecnologia.

>Denial of Service

Denial of Service, Negação de Serviço ou simplesmente DoS, consiste basicamente em tornar um sistema indisponível pela sobrecarga. Como analogia, podemos usar uma estrada bloqueada. É importante que os carros passem, mas não é possível, porque há um motorista que atrasa o fluxo dos demais carros.

>Botnet

Uma botnet, como o nome já indica, é uma rede de robôs ou, como deve-se imaginar, computadores que — ainda que os donos das máquinas não saibam — são controladas de forma central por um atacante. A analogia, neste caso, seria um grupo de carros que está bloqueando uma parte da estrada, porque os motoristas perderam o controle.
___

# #O grande problema
>Suponhamos agora que vários estradas estão bloqueadas, por diversos carros de diversos locais, ao longo do país inteiro. Esse é o DDoS.

{{< image src="../../../blog/static/ddos2.png" position="center" style="border-radius: 8px;" >}}

Um Distributed Denial of Service (DDoS) é uma espécie de DoS mais avançado, distribuído. Nesse caso, o inimigo usa uma botnet a seu favor, para aumentar a efetividade do ataque.

Como o atacante tem acesso a várias máquinas, espalhadas ao redor do mundo, os danos do ataque são muito maiores. Ele pode fazer com que o sistema simplesmente pare de funcionar ou pior.

Nem é preciso mencionar que os danos de um ataque desse tipo são enormes. Abaixo, vemos algumas das atitudes que esse invasor poderia tomar, aproveitando a instabilidade:

- Roubar informações, aproveitando a indisponibilidade;
- Instalar malwares no sistema;
- Usar o sistema-alvo como um novo bot na sua botnet, a fim de causar um ataque ainda maior;
- Ameaçar a empresa, pedindo dinheiro para interromper o ataque;
- E muito mais…
___

# #Exemplos reais (e recentes)
{{< image src="ddos3.png" position="center" style="border-radius: 8px;" >}}

A princípio, pode parecer um problema distante ou que ocorre com baixa frequência, mas o DDoS tem sido cada vez mais frequente nas manchetes.

>Veja comigo alguns exemplos recentes de DDoS. É possível que você se lembre ou até mesmo tenha sofrido com algum desses.

- Dezembro de 2014 — A PlayStation Network (PSN) sofre um ataque DDoS em pleno natal, impedindo que os usuários joguem ou comprem na loja.
- Outubro de 2016 — O provedor de DNS chamado Dyn sofre um ataque DDoS massivo que afeta vários sites populares, incluindo Twitter, Spotify, Netflix e Reddit.
- Setembro de 2017 — O Google sofre um dos maiores ataques DDoS da história.
- Fevereiro de 2020 — a gigante AWS informa que conseguiu mitigar um forte ataque DDoS em seus serviços.

Convivemos com o DDoS no dia-a-dia e, por vezes, não percebemos. Isso se dá porque há uma grande equipe trabalhando nos bastidores, para que a disponibilidade — ela mesma, da tríade CIA — seja reestabelecida.
___

# #Prevenção e Mitigação
{{< image src="../static/ddos4.png" position="center" style="border-radius: 8px;" >}}

>Mas, então, como se proteger? Como evitar que um ataque de tão grandes proporções ocorra ou, ainda que ocorra, evitar que atrapalhe as operações do negócio?

É recomendado, para evitar ou mitigar esse tipo de ataque, que seja implementada alguma solução que monitore a atividade na rede, a fim de bloquear o máximo de tráfego suspeito possível. Essas soluções incluem:

- Firewalls com regras de controle de acesso, IPS (Intrusion Prevention Systems), para automaticamente bloquear o tráfego indesejado;
- Usar um sistema de Load Balance, para que o tráfego da rede seja distribuído e não fique concentrado em um único servidor. Assim, evitamos um ponto único de falha.
- Treinamento, afinal, há sempre o fator humano na equação. Os funcionários, a equipe de redes e de resposta a incidentes devem estar preparados para que, ainda que ocorra um DDoS, ele tenha o mínimo de impacto na companhia.
- E, claro, manter todos os sistemas atualizados com os patches mais recentes, a fim de minimizar as vulnerabilidades.

Com isso, é possível diminuir as chances desse tipo de ataque, ainda que “segurança total” ou “zero falhas” sejam termos quase folclóricos.

# #Conclusão
Concluo propondo a seguinte reflexão:

>_Muito se fala sobre a importância da disponibilidade do sistema, e com razão. De fato, esse tema deveria ser muito mais propagado e debatido._

>_Mesmo assim, devemos lembrar que a Segurança é a maior aliada da Disponibilidade. Sem segurança, qualquer ataque ou incidente pode causar interrupções no funcionamento dos serviços para os usuários, amplificando ainda mais os danos e o prejuízo, que pode ser irreversível._

>**Pode, nos dias de hoje, uma empresa sobreviver sem cybersecurity?**
___
Muito obrigado pela sua companhia até aqui, querido(a) leitor(a)! 