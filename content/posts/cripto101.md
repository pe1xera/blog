+++
title = 'Cripto101 - Uma abordagem sem Alice e Bob'
date = 2024-03-24
cover = "cripto101_cover.png"
+++

Imagine que Alice e Bob m0rreram. Por favor, não se espante! Caso prefira, imagine que eles tiraram suas tão sonhadas férias. Esses dois conhecidos personagens foram os nossos companheiros por muito tempo, durante o estudo de Criptografia, mas é hora de descansarem.  

O objetivo deste artigo é introduzir alguns conceitos de criptografia, sem incorrer na monotonia e falta de criatividade que assolam os nossos tempos. Portanto, não espere ver sequências enormes de detalhamentos históricos ou uma quantidade (fora do normal) de termos técnicos.   

Considere a leitura como um mero convite para o estudo mais aprofundado, jamais como um parâmetro universal ou como uma verdade autossuficiente. Se possível, dê sugestões e critique até os erros gramaticais, porque é assim que crescemos.

---

# Criptografia

Criptografia é, por essência, um tema complexo. Por mais que a ideia de uma "técnica de ofuscação ou encriptação de informações" (Fortinet)¹ seja simples, a quantidade de algoritmos, cifras e conceitos tende a causar uma natural - e perigosa - confusão.

Encriptação envolve a Confidencialidade dados. Normalmente, isso é feito encriptando um arquivo com uma senha mas, ao mesmo tempo, uma senha fácil de adivinhar como "rodrigo2024" não vai fornecer nenhuma segurança confiável. Por conta disso, tem-se algoritmos criptográficos, que também podem ter suas fraquezas.

# Hashing  

Primeiramente, hashing não tem nada a ver com encriptação. Porém, frequentemente aparece em conexão com ela. Essa confusão é entendível, devido às características que um hash possui.

Uma função de hash nada mais é do que um cálculo - sim, um cálculo - que produz uma saída de tamanho fixo, a partir de qualquer entrada. Se a entrada mudar, ainda que minimamente, a saída será totalmente diferente. Isso faz com que possamos rastrear qualquer mudança no arquivo, mesmo que seja a mais mínima manipulação. 

Essa propriedade permite que os hashes sejam usados especialmente para checagens de integridade. Abaixo, temos o hash gerado da pintura "Jesus and Peter on the Water", de Gustave Brion. 

{{< image src="../../../jesus_e_pedro.png" position="center" style="border-radius: 2%;" title="Arquivo original importado no Photoshop." >}}   

{{< image src="../../../jesus_hash_original.png" position="center" style="border-radius: 2%;" title="Arquivo com pequena modificação na parte inferior." >}}   

>md5sum jesus_e_pedro.png  
>2bf92a6e8cf03491bac344256c33cfc1  
>jesus_e_pedro.png

Porém, caso façamos uma pequena modificação na imagem, como abaixo, incluindo o texto "só Cristo salva", veremos que o resultado do hash, usando a mesma função, é completamente diferente. O mesmo aconteceria caso o texto inserido estivesse embbedado na imagem e invisível aos olhos, mas esteganografia é um assunto para outro momento.

{{< image src="../../../jesus_e_pedro2.png" position="center" style="border-radius: 2%;" title="Modificação de poucos pixels realizada na imagem." >}}   

{{< image src="../../../hash_novo.png" position="center" style="border-radius: 2%;" title="Hash do arquivo novo gerado com o md5sum é totalmente diferente da imagem original." >}}    

>md5sum jesus_e_pedro2.png                                                             
>f416c78504c9abca11049bbfbe4c988c   
>jesus_e_pedro2.png  

Apesar disto, a melhor parte do Hash é que os dados originais não podem ser reconstruídos a partir da saída, trata-se de uma função de via única, tecnicamente irreversível. Normalmente, só se consegue encontrar o equivalente de um hash em um serviço de lookup como o [hashes.com](https://hashes.com/en/decrypt/hash).

befd1ea261d11ae5ba4f3f0363313c52:**Hashing**

---   

# Codificação

Codificação (ou Encoding), por sua vez, não é encriptação, ainda que se pareça às vezes. Codificação é uma forma de representar caracteres usando outro sistema. Por exemplo, o binário é uma outra forma de representar um número que existe no sistema decimal. Se um número for atribuído a uma letra, ela também poderia ser representada em binário.

"Saquei", em binário, seria "01010011 01100001 01110001 01110101 01100101 01101001". Ainda que você não consiga ler mais e pareça encriptado, é só a conversão de uma forma de representação para outra. Ele pode ser traduzido de volta usando as mesmas regras. Vale lembrar que, por isso, codificação são traz nenhuma confidencialidade.

Um exemplo muito famoso é o base64 (o terror dos CTFs). Ele é usado para transferir os dados que contenham bytes que não existem em ASCII sem codificação. Normalmente, se parece como algo assim:

>RXNzYSBnZW50ZSBpbnZlbnRhIGNhZGEgY29pc2EsIHZpdT8K=

{{< image src="../../../base64_exemplo.png" position="center" style="border-radius: 2%;" title="Exemplo de texto base64 decodificado." >}}  

---

# Cifra de César

Pois bem, vamos falar de criptografia de verdade. Aqui, o princípio é bem simples e trata-se de um método simétrico de encriptação. Por ser um dos métodos mais simples e menos seguros, hoje em dia, a cifra de César é usada principalmente para ilustrar os princípios básicos da criptologia. Durante a encriptação, cada letra do texto claro é mapeada a uma letra do texto cifrado.

>Entendi foi nothing   
>Lualukp mvp uvaopun     

Para a decriptação, o alfabeto é rotacionado para a posição oposta, usando o mesmo número de caracteres. A imagem abaixo torna mais claro o entendimento.  

{{< image src="../../../caesar.png" position="center" style="border-radius: 2%;" title="Ilustração visual da Cifra de César." >}}  

Obviamente, a cifra de substituição é muito simples e não fornece a segurança necessária contra a decifragem não autorizada e pode ser, facilmente, "quebrada" por qualquer um que perceba o padrão.

---

# Cifra de Bloco - ECB

Agora, vamos um pouco mais na direção da criptografia. O Advanced Encryption Standard (AES) é, basicamente³, considerado como um algoritmo de encriptação segura. Porém, ele pode ser operado de vários modos.

O modo mais simples e, também, o mais inseguro, é o Electronic CodeBook (ECB). Aqui, o texto claro é dividido entre blocos de tamanhos iguais, cada um deles criptografado com a chave. Isso faz com que os blocos possam ser encriptados paralelamente, portanto é uma criptografia mais rápida.

{{< image src="../../../funcionamento_ecb.png" position="center" style="border-radius: 2%;" title="Funcionamento do ECB." >}}  

Por mais que o AES seja bom, esse modo, em especial, tem suas fraquezas. Isso porque padrões podem ser detectados quando vários blocos no texto plano são iguais. Os mesmos blocos são criptografados da mesma forma, o que permite tirar conclusões sobre o texto simples durante a criptoanálise. 

Na imagem abaixo, usando como exemplo a pintura "Paul Preaching to the Thessalonians", de Gustave Doré, temos uma visão clara do funcionamento do AES no modo ECB.

{{< image src="../../../aes_ecb.png" position="center" style="border-radius: 2%;" title="Ilustração visual do AES ECB." >}}  

Perceba que, apesar de criptografada, a imagem repete alguns padrões de cores. Isso ocorre, justamente, porque os blocos de cores iguais são criptografados da mesma forma (a chave é a mesma). Deste modo, fica mais fácil entender aquilo que estamos visualizando.

---

# Cifra de Bloco - CBC

Para resolver a limitação do modo ECB, o modo Cipher Block Chaining (CBC) foi desenvolvido. Neste modo, os blocos continuam sendo criptogrados individualmente, mas são encadeados de forma que padrões não são mais reconhecíveis. Para isso, é usado o chamado Vetor de Inicialização (IV) no iinício do processo e cada bloco é vinculado ao anterior. 

Explicando de maneira grosseira, mas didática - espero eu - poderíamos dizer que os blocos são produzidos usando o bloco anterior (já cifrado) + o texto plano atual⁴. Abaixo, temos uma melhor visualização deste conceito.  

{{< image src="../../../funcionamento_cbc.png" position="center" style="border-radius: 2%;" title="Funcionamento do CBC." >}}  

Como podemos ver na imagem abaixo, este algoritmo faz uma encriptação completa. Como deve ser!

{{< image src="../../../aes_cbc.png" position="center" style="border-radius: 2%;" title="Ilustração visual do AES CBC." >}}  

Ainda assim, temos que ter em mente que criptografia sozinha não é o suficiente para proteger os dados de manipulação. É importante lembrar que mesmo dados criptografados podem ser modificados, apesar da encriptação. Isso significa que, quando o dado for decriptado, o resultado será diferente do texto plano.

---

# Epílogo

Aqui entrariam outros mecanismos de segurança, pois vemos cada vez mais ataques aos algoritmos modernos, péssima manipulação das chaves e más configurações das aplicações e sistemas; um prato cheio para um operador malicioso. 

Agradeço pela leitura até aqui, querido leitor. Cheque as referências e até a próxima!

---

# Recomendações (e referências)

Permita-me deixar, como principal recomendação, o curso que inspirou a escrita deste artigo: **Criptologia I**, da San Jose Institute of Technology (SJIT), ensina criptografia e criptoanálise por meio de uma abordagem não-matemática (apenas lógica), com foco em esquemas visuais, ilustrações e atividades práticas (e nada de Alice e Bob).  
1. [Criptologia I - SJIT](https://on.sanjose.institute/courses/criptologia-i)   

{{< image src="../../../criptologia.png" position="center" style="border-radius: 2%;" title="Curso do SJIT." >}}   

Estamos falando de um conteúdo raríssimo, ainda mais quando falamos de recursos em PT-BR. O material serve como um excelente handbook, para reler e consultar quando necessário (e sabemos que será necessário).   

Demais referências:   
2. [What is Cryptography? - Fortinet](https://www.fortinet.com/resources/cyberglossary/what-is-cryptography)  
3. [What Is AES Encryption? The Complete Guide - Javed Shah](https://www.1kosmos.com/authentication/aes-encryption/)   
4. [Cryptographic Standards and Guidelines- NIST](https://csrc.nist.gov/projects/cryptographic-standards-and-guidelines/archived-crypto-projects/aes-development)  
5. [Álbum escutado durante a escrita](https://open.spotify.com/playlist/2sj2Cyk1QsDZtNA1R2DQLe?si=974ceadd048d49b5)  