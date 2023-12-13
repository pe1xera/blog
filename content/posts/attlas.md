+++
title = 'Construindo o aTTLas portscanner'
date = 2023-12-11
cover = "scripting.png"
+++


_“Se você não consegue fazer algo bom, pelo menos faça com que pareça bom.”_   
_~Bill Gates_

---

# Intenção

Com base no conteúdo ensinado pelo mestre Longatto no curso Novo Pentest Profissional e outros materiais complementares que encontrei pela internet a fora, resolvi criar um script em Python que faça o escaneamento de portas TCP abertas em um determinado host, respeitando alguns princípios como: Apresentação, Usabilidade e Agilidade, dentro - é claro - dos limites do pouco que conheço. 

Em termos de etimologia, atlas é o nome que se dá a uma coleção de mapas em que estão representadas as posições das estrelas. Também é este o nome dado pela mitologia grega ao titã condenado a carregar o peso dos céus em suas costas por toda a eternidade. TTL, por sua vez, é uma referência ao Time To Live, um campo usado no datagrama IP como um contador do tempo de vida de um pacote.

---
# Princípios


Surge, então, o **"aTTLas"**, um simples portscanner em Python, desenvolvido no método que apelidei de 'scripting like a n00b' - o qual é autoexplicativo.

O aTTLas não tem a pretensão de ser melhor do que qualquer script existente e sequer ser comparável a qualquer deles, servindo apenas como um método para colocar em prática aquilo que aprendi, servindo como minha primeira ferramenta autoral. 

Dito isso, querido leitor, também não se trata de um script estéril e sem utilidade prática. Na realidade, aTTLas pode ser bastante plausível, a depender das suas intenções. O script tem sua própria filosofia e segue três princípios norteadores básicos:

> 1) Apresentação

{{< image src="../../../attlas1.gif" position="center" style="border-radius: 5%;" >}}   

Algo que me encantou e ainda encanta nas ferramentas de segurança de linha de comando são as ASCII arts que permeiam as melhores delas. Neste caso, os banners de entrada e saída no aTTLas remetem ao mar e as estrelas, transportando o usuário para este "universo", onde ele pode se sentir um marinheiro ou faroleiro observando as estrelas, que representam as portas abertas no alvo.

Enquanto funciona, o script exibe uma pequena animação, de forma que o usuário não tem de esperar, estático, por alguma informação na tela. Ele pode ser ~~~engabelado~~~ conduzido a uma melhor experiência visual enquanto espera a conclusão da tarefa do script.

> 2) Usabilidade

Dado que o script não possui uma ampla gama de opções, não há a necessidade de trabalhar com muitos argumentos, uma escolha mais estética do que lógica. Neste caso, o usuário deve selecionar entre as três opções disponíveis dentro do programa, sendo elas: Top 100, Top 1000 e todas as portas, passando ao programa a sua escolha como argumento, junto ao endereço do alvo.  
Ex.: ```./aTTLas.py businesscorp.com.br 100``` - Escaneia as 100 portas TCP mais comuns no alvo businesscorp.com.br.

{{< image src="../../../attlas2.gif" position="center" style="border-radius: 5%;" >}}   

As portas estão diretamente inseridas no código e foram obtidas por meio de uma lista contendo as portas principais escaneadas pelos scripts mais robustos e estão listadas diretamente no programa, uma solução que possivelmente poderia ser melhor, como obtendo uma lista de portas por wordlist, mas não vem ao caso. A exceção é o caso de varredura em todas as portas, em que foi criado um looping com este objetivo.


> 3) Agilidade*

Tempo é importante. Um port scanner muito lento é inútil, já que um de seus objetivos é a eliminação do trabalho e as validações manuais. Definimos o timeout padrão de 0.5 segundos - usando ```socket.setdefaulttimeout(0.5)``` - a fim de dar tempo para que as requisições sejam processadas, mas sem exageros na validação de cada uma das portas.

{{< image src="../../../attlas_code.png" position="center" style="width: 80%; border-radius: 5%;" >}}   

No entanto, por se tratar de uma versão inicial do script e, levando em consideração que ainda não tenho domínio da linguagem, a agilidade não está no melhor estágio em que poderia. Abordamos as limitações do código adiante.

---

# Limitações

Certamente, seria possível ter um script mais rápido, utilizando multi-threading e outros aspectos da linguagem, sobre os quais preferi não me aventurar neste primeiro momento, mas que já me despertaram interesse e podem, sem dúvidas, ser aplicados no mesmo script futuramente. 

A condição ```== 0``` no código indica que não houve erros durante a tentativa de conexão, indicando que a porta está "aberta". No entanto, é importante observar que essa abordagem tem limitações, pois uma porta pode estar aberta e apresentar diferentes comportamentos. Este scanner não abrange todos os cenários possíveis e não é capaz de realizar validações mais abrangentes sobre o estado da porta, como a detecção de portas filtradas, por exemplo. 

---

# Conclusão e Aprendizados

{{< image src="../../../attlasenc.gif" position="center" style="border-radius: 5%;" >}}   

Por mais que o aTTLas não seja o melhor dos scripts e, pelo contrário, peca em diversos aspectos, acredito que o simples fato de pesquisar alguns conceitos da linguagem para desenvolvê-lo me fez entender muito melhor os aspectos do Python e suas bibliotecas. Certamente usarei meu próprio código em CTFs ou contextos semelhantes.

Agradeço por sua leitura até aqui, querido leitor!