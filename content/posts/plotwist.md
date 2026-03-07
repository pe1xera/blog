+++
title = "Plot Twist (ou: Kishōtenketsu)"
date = 2026-03-06
cover = "plotwist.png"
images = ["plotwist.png"]
+++

### Um vício antigo

Pessoas que operam na cibersegurança, por vezes desenvolvem um vício em padrões. É quase um defeito de fábrica: o sujeito começa a buscar correlações em tudo, tentando antecipar todas as coisas antes de acontecerem (até o que não é trabalho). O problema é que, às vezes, esse tipo de atitude é bastante prejudicial, porque nem tudo na vida segue um fluxograma.  

Particularmente, sempre gostei de criar histórias. Muito embora eu guarde para mim, fico muito satisfeito em ver o resultado delas. A melhor parte é sempre o **Plot Twist**, justamente quando ocorre alguma reviravolta na história e ela muda completamente o seu curso.   

Na estrutura das histórias orientais, isso é chamado de *"Ten"*, e está dentro do conceito de **Kishōtenketsu**, mas não se assuste, porque é mais simples do que parece. Basta quebrar a palavra em partes:

- **Ki (起): Introdução** – Apresenta os personagens e o cenário, estabelecendo o contexto da história.
- **Sho (承): Desenvolvimento** – Expande a introdução, aprofundando a história e os elementos apresentados.
- **Ten (転): Reviravolta** – Introduz um elemento inesperado que muda a direção da narrativa.
- **Ketsu (結): Conclusão** – Conecta todos os pontos e encerra a história de forma coesa.

Perceba que essa técnica não depende de um conflito, mas sim de uma grande mudança na narrativa, seja ela qual for. Agora, como isso se conecta com segurança, você se pergunta? Bom, acontece que Defesa Cibernética é, no fundo, uma eterna tentativa de controlar o ambiente e mitigar os impactos desse Plot Twist, o nosso "Ten".

{{< image src="../../../plotwist.png" >}} 

### Uma questão atual

Por isso que grande parte do trabalho  do Blue Team gira em torno de algo que parece simples, mas é absurdamente difícil na prática: estabelecer o que é normal. Ah, palavra terrível essa: normal.

Em segurança, chamamos isso de baseline. Antes de identificar o inesperado, é preciso conhecer profundamente o comportamento esperado do sistema, obviamente. Qual é o volume normal de tráfego? Que processos costumam rodar? Em que horário certos usuários fazem login? Que arquivos mudam com frequência e quais praticamente nunca deveriam mudar?

Quando você tem essa linha de base bem definida, o “Ten” começa a aparecer com mais clareza.

Um exemplo clássico é a detecção de malware baseada em comportamento. Durante muito tempo, antivírus dependeram quase exclusivamente de assinaturas de hash. A lógica era simples: se o hash do arquivo está na base de dados, então ele é malicioso. Se não está, provavelmente é benigno.

O problema é que basta uma pequena alteração no binário para gerar um hash completamente diferente. Para quem está do lado ofensivo, isso é tranquilo de executar. Já pra quem está defendendo, significa que o ataque pode passar completamente despercebido (principalmente para os escravos de ferramentas). 

### Uma solução futura

Em vez de olhar apenas o que o arquivo é, por exemplo, seria interessante a observar o que ele faz. Um processo que, logo após ser executado, tenta modificar arquivos sensíveis do sistema, abrir conexões externas estranhas e persistir no boot da máquina? Isso não precisa nem de hash para levantar suspeitas. O comportamento já diz muita coisa.

Essa mudança de perspectiva é, de certa forma, uma tentativa de lidar com o inevitável “Ten”, porque, no fim das contas, não importa o quanto tentemos prever tudo com regras e assinaturas, sempre vai existir um momento em que algo inesperado acontece. 

E quando isso acontece, a história muda de direção, restando saber como lidar com ela. Ora, eu não procuro responresolver isso aqu e também acho que nenhum de nós pode ser orgulhoso o suficiente para dizer que tem a resposta deste grande enigma.

Não, este texto não é sobre literatura.  
Não, também não é sobre cibersegurança.   

É sobre as escolhas da vida, sobre a tendência bizarra do ser humano de cometer os mesmos erros de sempre, e sobre como Deus conduz os seus filhos no melhor caminho, apesar de sua inclinação para repetir os mesmos vacilos.

---

Obrigado pela leitura até aqui, querido leitor!