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
"befd1ea261d11ae5ba4f3f0363313c52"

Primeiramente, hashing não tem nada a ver com encriptação. Porém, frequentemente aparece em conexão com ela. Essa confusão é entendível, devido às características que um hash possui.

Uma função de hash nada mais é do que um cálculo - sim, um cálculo - que produz uma saída de tamanho fixo, a partir de qualquer entrada. Se a entrada mudar, ainda que minimamente, a saída será totalmente diferente. Isso faz com que possamos rastrear qualquer mudança no arquivo, mesmo que seja a mais mínima manipulação. 

Essa propriedade permite que os hashes sejam usados especialmente para checagens de integridade. Abaixo, temos o hash gerado da pintura "Jesus and Peter on the Water", de Gustave Brion. 

{{< image src="../../../jesus_e_pedro.png" position="center" style="border-radius: 2%;" alt="Arquivo original importado no Photoshop" >}} 
{{< image src="../../../jesus_hash_original.png" position="center" style="border-radius: 2%;" alt="Arquivo com pequena modificação na parte inferior" >}} 

>md5sum jesus_e_pedro.png  
>2bf92a6e8cf03491bac344256c33cfc1  
>jesus_e_pedro.png

Apesar disto, a melhor parte do Hash é que os dados originais não podem ser reconstruídos a partir da saída, trata-se de uma função de via única, tecnicamente irreversível. 

9134fdd1f231cfbbcf45df3c41a2d706:**Codificacao**

Criptografia é Encriptação
Codificação base 64


---


# Referências (e recomendações)

1. [What is Cryptography - Fortinet](https://www.fortinet.com/resources/cyberglossary/what-is-cryptography)
