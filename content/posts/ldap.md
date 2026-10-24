+++
title = "Lightweight Directory Access Protocol (LDAP)"
date = 2026-10-23
cover = "ldap.png"
images = ["ldap.png"]
+++

Querido leitor, há uma diferença considerável entre olhar para um log e conseguir lê-lo. Reconhecer o nome de uma operação ajuda, claro, mas não basta para entender por que ela aconteceu, o que o cliente pediu ao servidor e se aquela conversa combina com o comportamento esperado do ambiente.

Neste texto, quero olhar para o LDAP junto com você, e faremos isso do ponto de vista de quem precisa defender um ambiente, acompanhando a conversa entre os dois lados. Deus sabe que gosto muito de teoria, mas também gosto dos bytes e dos logs; então vamos aliá-los para tirar um maior proveito dessa brincadeira.

Como de costume, sou totalmente aberto a correções, quanto a erros técnicos e gramaticais, e fico feliz caso alguém os aponte para mim. Segurança é uma área que exige curiosidade, mas exige também humildade para rever o que julgamos saber e talvez estejamos errados.

---

## Era uma vez uma árvore

O LDAP não surgiu do nada. O nome em si já é um mini-spoiler, vejamos: “*Lightweight Directory Access Protocol”*, que (em tradução livre) seria algo como um “protocolo leve para acessar diretórios”. Um DAP, porém com "L" de leve! O diretório ao qual ele se refere é o **X.500**, uma família de padrões desenvolvida no âmbito do CCITT, hoje ITU-T (International Telecommunication Union), e da ISO/IEC.

O X.500 foi pensado para oferecer um serviço de diretório em larga escala, entre outras coisas para localizar nomes e endereços ligados ao antigo padrão X.400. A proposta era que se tivesse entradas organizadas em um formato de árvore, regras para descrever seus atributos e protocolos diferentes para acessar, distribuir e replicar as informações. Tudo isso seguindo o modelo OSI.

Como sabemos, esse tipo de padrão nunca é desenvolvido somente por uma pessoa, então vamos dar nome aos bois, pois nada mais justo do que dar os créditos a quem tem o direito.

Tudo começa em Londres, onde **Steve Kille** trabalhava no ISODE Consortium. Junto com ele estavam **Tim Howes**, da Universidade de Michigan, e **Wengyik Yeong**, da Performance Systems International. Os três compartilhavam um incômodo comum: o X.500 era elegante no papel, mas pesado demais na prática.

Para entender esse incômodo, precisamos dar um passo atrás. O X.500 foi projetado dentro do modelo OSI, a famosa pilha de sete camadas que dominou o imaginário da computação nos anos 80. Naquela visão de mundo, hoje ultrapassada (de certo modo), cada protocolo deveria ter sua sessão, sua apresentação, seu controle formal. O resultado era que uma simples consulta a um diretório exigia uma sequência de negociações e handshakes que deixava qualquer aplicação lenta e inchada.

A ideia de Kille, Howes e Yeong foi quase herética para a época: **e se simplificássemos o transporte, mas mantivéssemos a essência do modelo de dados?** Ou seja, em vez de carregar toda a pilha OSI, eles colocariam os elementos do diretório diretamente sobre o TCP. Em vez de codificações exóticas, usariam algo já conhecido, o BER. O protocolo continuaria falando a mesma língua do X.500 (a mesma árvore, os mesmos atributos), mas de um jeito que uma aplicação simples pudesse implementar em poucos dias.

O resultado saiu como a **RFC 1487**, em julho de 1993. O nome dizia tudo: *Lightweight Directory Access Protocol*, em tradução livre: um "protocolo leve para acessar diretórios". Leve em relação ao X.500, não em relação ao que viria depois.

Com o tempo o protocolo evoluiu: o RFC 1487 foi substituído pelo RFC 1777 (LDAPv2) e, mais tarde, chegou a versão que sustenta praticamente tudo o que vemos hoje, o **LDAPv3** (RFC 4511). 

---

## O que é um diretório, afinal?

A palavra "diretório" carrega uma ambiguidade perigosa. No dia-a-dia, pensamos logo em pastas de arquivos. Em LDAP, é mais como um **banco de dados especializado em leitura**, otimizado para consultas e não para escrita. Pense na Lista de Endereços do Outlook. No dia a dia, ninguém "edita" esse diretório, só consulta. Busca-se o nome de um colega, o e-mail de um setor, o ramal de alguém. As atualizações existem (como quando alguém é contratado, muda de time ou sai da empresa), mas elas são raras, controladas e feitas por quem administra, não por quem consulta. O LDAP é a engrenagem que, por baixo dos panos, faz esse tipo de diretório funcionar.

A diferença entre um banco de dados, que conhecemos bem, e um diretório está na **forma** dos dados. Um banco relacional organiza tudo em tabelas com colunas rígidas. Um diretório organiza tudo em uma **árvore hierárquica**, onde cada nó tem um nome e um conjunto de atributos.

Antes de seguir, vejamos o diagrama abaixo. Ele mostra a estrutura conceitual que o LDAP usa, e que o Active Directory herdou quase inteiramente.

```
                       [dc=empresa,dc=com]          ← raiz do domínio
                                |
                +---------------+---------------+
                |                               |
      [ou=Usuarios]                      [ou=Computadores]
                |                               |
        +-------+-------+               +-------+-------+
        |               |               |               |
 [cn=bilbo]      [cn=tauriel]     [cn=PC-BILBO]   [cn=SRV-SMAUG]
```

Cada linha dessa árvore é uma **entrada** (*entry*). Cada entrada tem um **nome único** que a identifica na árvore (o *Distinguished Name*, ou DN), além de um conjunto de **atributos** que descrevem o que aquela entrada é, como nome, e-mail, telefone, senha e grupos.

Quando abrimos o "Active Directory users and Computers" no Windows, estamos vendo essa árvore renderizada. Quando uma ferramenta consulta o AD, está caminhando por ela.

---

## Um pseudo-CPF da entrada

Aqui chegamos no primeiro conceito que precisa ficar cravado, porque ele vai aparecer em **todo** log e **toda** captura de pacote daqui pra frente, o **DN** (*Distinguished Name*, ou Nome Distinguido).

O DN é o endereço completo de uma entrada na árvore. Ele é escrito da entrada mais específica para a mais genérica, separado por vírgulas. Voltando ao diagrama anterior, o DN do usuário Bilbo aparece assim.

```
cn=bilbo,ou=Usuarios,dc=empresa,dc=com
```

Lê-se da direita para a esquerda, começando pelo domínio e terminando na entrada.

- `dc=com` → faz parte do domínio `.com`
- `dc=empresa` → no domínio `empresa.com`
- `ou=Usuarios` → dentro da unidade organizacional "Usuarios"
- `cn=bilbo` → a entrada do usuário Bilbo

Cada uma dessas siglas tem um significado que vale memorizar, como mostra a tabela a seguir.

| Sigla | Significado | Exemplo |
| --- | --- | --- |
| `dc` | *Domain Component* | `dc=empresa` |
| `ou` | *Organizational Unit* | `ou=Usuarios` |
| `cn` | *Common Name* | `cn=bilbo` |
| `uid` | *User ID* | `uid=bbaggins` |

O DN é o equivalente LDAP do que um CPF é para uma pessoa, pois não importa quantos "Bilbos" existam, o DN de cada um é único. É por isso que todo `BindRequest` (autenticação) e todo `SearchRequest` (consulta) têm um DN envolvido. Ele é a chave que localiza o nó na árvore.

Vale notar que a mesma árvore pode conter usuários como `cn=tauriel` e `cn=thorin` na `ou=Usuarios`, e contas privilegiadas como `cn=gandalf` em uma `ou=Admins`. O DN de cada um segue a mesma lógica, mudando apenas o caminho até a raiz.

---

## A conversa entre cliente e servidor

Agora que sabemos o que existe dentro do diretório, podemos entender **como** as coisas conversam com ele.

Toda comunicação LDAP é uma **conversa** entre dois lados, e isso é importante, porque facilita o entendimento. Temos, então, o **cliente** (que quer algo) e o **servidor** (que tem os dados). O protocolo define que essa conversa acontece em ciclos de **requisição e resposta**, sempre na mesma estrutura.

```
   CLIENTE                                       SERVIDOR
     |                                              |
     |---- Requisição (messageID=1, operação) ----->|
     |                                              |
     |<--- Resposta  (messageID=1, resultado) ------|
     |                                              |
```

Há três coisas importantes nesse diagrama. Primeiro, **toda requisição tem uma resposta**. Não existe requisição "silenciosa". Isso é ouro para a análise, pois se uma requisição sai mas a resposta não volta, ou o pacote se perdeu, ou alguém está bloqueando, e isso por si só é um sinal.

Segundo, **o `messageID` correlaciona tudo**. Cada requisição leva um número de identificação único. A resposta carrega o mesmo número. Em uma captura de pacotes com milhares de mensagens, é o `messageID` que diz qual resposta pertence a qual pergunta. Sem ele, seria uma bagunça.

Terceiro, **o "verbo" da operação muda**. A estrutura é a mesma, mas o conteúdo da requisição diz o que o cliente quer fazer. E é aí que entram as operações.

---

## As duas operações que precisamos conhecer

O LDAP define cerca de uma dúzia de operações, como adicionar, modificar, excluir, comparar e abandonar. Mas para quem está começando na análise, **duas** concentram 90% do que veremos em logs e capturas.

### BindRequest, o "aperto de mão" de autenticação

Toda sessão LDAP começa com um **Bind**. É o momento em que o cliente se apresenta ao servidor e diz *"sou eu, aqui estão minhas credenciais"*. Sem um Bind (ou com um Bind anônimo), o servidor não vai entregar muita coisa.

O BindRequest carrega dois elementos essenciais. O primeiro é o **DN** da entrada que está tentando se autenticar, ou seja, quem é. O segundo é a **credencial**, que em geral é uma senha, mas pode ser um certificado, um ticket Kerberos, ou simplesmente *nada* (bind anônimo).

O que o servidor devolve é um **BindResponse** com um código de resultado.

| Código | Significado |
| --- | --- |
| `success` (0) | Autenticou |
| `invalidCredentials` (49) | Usuário ou senha errados |
| `noSuchObject` (32) | O DN informado não existe |

**Por que isso importa para o SOC?** Porque é aqui que ataques de força bruta, *password spraying* e enumeração de usuários acontecem. Um `noSuchObject` repetido significa que o atacante está testando nomes de usuário para ver quais existem, e pode estar tentando `cn=bilbo`, `cn=tauriel`, `cn=thorin`, `cn=gandalf`, e assim por diante. Um `invalidCredentials` repetido significa que ele já sabe que o usuário existe e está chutando a senha. A distinção entre os dois códigos é a diferença entre "descobrindo o terreno" e "atacando".

### SearchRequest, a operação mais comum e a mais ruidosa

Depois de autenticado, o cliente quase sempre vai querer **buscar** algo. É o `SearchRequest`. E é aqui que a maior parte do volume de logs LDAP nasce.

Um SearchRequest é composto por alguns parâmetros que determinam o que volta, como mostrado a seguir.

```
   SearchRequest
   ├── baseObject: "dc=empresa,dc=com"     ← de onde começar a busca
   ├── scope: wholeSubtree (2)             ← até onde descer na árvore
   ├── filter: (objectClass=user)          ← o que procurar
   └── attributes: ["cn", "mail"]          ← o que trazer de volta
```

Vamos dissecar cada um deles.

**`baseObject`** é o ponto de partida. Pode ser a raiz do domínio (`dc=empresa,dc=com`), uma OU específica (`ou=Usuarios,dc=empresa,dc=com`), ou até uma única entrada (`cn=bilbo,ou=Usuarios,dc=empresa,dc=com`).

**`scope`** diz o quão fundo descer a partir do `baseObject`.

| Scope | Valor | O que faz |
| --- | --- | --- |
| `baseObject` | 0 | Só consulta a entrada base, sem descer |
| `singleLevel` | 1 | Desce um nível (filhos diretos) |
| `wholeSubtree` | 2 | Desce **todos** os níveis (subárvore inteira) |

**`filter`** é o coração da busca. É a "condição WHERE" do LDAP. Um filtro como `(objectClass=user)` retorna tudo que é usuário. Um filtro como `(&(objectClass=user)(adminCount=1))` retorna só os administradores, incluindo, talvez, o `cn=gandalf`. Um filtro como `(sAMAccountName=bilbo)` retorna o usuário Bilbo, se existir.

O filtro tem sua própria sintaxe, e encontraremos variações dele nos logs.

```
(objectClass=user)                        → igualdade simples
(&(objectClass=user)(memberOf=Grupo))     → AND de duas condições
(|(cn=bilbo)(cn=tauriel))                 → OR
(!(objectClass=computer))                 → NOT
(sAMAccountName=bil*)                     → wildcard (substring)
```

**`attributes`** é a lista do que o cliente quer receber de volta. Se ele pedir `["cn", "mail"]`, o servidor devolve só esses campos. Se pedir `["*"]`, devolve **todos** os atributos, e é aí que a coisa começa a ficar interessante para a análise.

---

## O que essa conversa deixa de rastro

Uma vez entendida a conversa, podemos olhar para os logs com outros olhos. Quando um cliente faz uma busca e o servidor responde, esse diálogo pode deixar vestígios em vários lugares. Os dois principais merecem atenção.

### 1. A captura de rede

Tendo visibilidade de rede, vemos a conversa crua. No Wireshark, um SearchRequest aparece assim, de forma simplificada.

```
Lightweight-Directory-Access-Protocol
    messageID: 5
    protocolOp: searchRequest (3)
        baseObject: "dc=empresa,dc=com"
        scope: wholeSubtree (2)
        filter: (objectClass=user)
        attributes: cn, mail
```

Isso é ouro, pois vemos a intenção exata do cliente. Mas essa visibilidade depende de estarmos capturando o tráfego, o que nem sempre é viável em escala.

### 2. Os logs do servidor

O Active Directory registra buscas LDAP no **Event ID 1644**, quando a consulta "custa caro" o suficiente para justificar um registro. Os critérios são ajustáveis (tempo de processamento, número de entradas visitadas), mas por padrão o 1644 aparece quando o servidor acha que a busca foi pesada.

O evento registra o **DN base** da busca, o **filtro** que foi usado, o **cliente** de origem (IP), o **número de entradas** que a busca visitou e o **tempo** de processamento.

Para o analista, o 1644 é a fonte de telemetria mais acessível. Mas ele tem um problema que precisa ser entendido em camadas.

---

## As coisas podem sair do controle

Aqui está a armadilha em que muitos analistas caem, **confiar apenas no Event ID 1644**. A intuição é razoável, pois parece que "se alguém está enumerando o AD, o 1644 vai pegar". Mas essa intuição é falsa por razões estruturais, não por má configuração.

Vamos entender por quê, um caso por vez, sem pressa.

### Caso 1, o Bind não gera 1644 (e o Search pode não gerar)

O primeiro detalhe é contraintuitivo, **o `BindRequest` não gera Event ID 1644**. Esse evento é gerado apenas para operações de **busca**. Ou seja, o momento em que o atacante tenta autenticar com senhas chutadas não aparece no 1644. Ele aparece em outros eventos (4624/4625 nos logs de segurança do Windows), mas no LDAP puro, o Bind passa silencioso.

O segundo detalhe é que nem toda busca gera 1644. Se a busca for "barata" (poucas entradas visitadas, tempo curto), o servidor não registra nada. Isso significa que um atacante inteligente pode **diluir suas buscas** em consultas pequenas e nunca disparar o gatilho.

```
   Atacante ingênuo:              Atacante cuidadoso:
   ------------------             ------------------
   Uma busca                     Muitas buscas
   com scope=subtree             com scope=base
   retornando 10.000             retornando 1 entrada
   entradas                      cada
        |                              |
        v                              v
   Event 1644 gerado             Nenhum 1644 gerado
   (visível)                     (invisível)
```

### Caso 2, o LDAP Ping nem chega ao motor LDAP

Existe uma operação especial no Active Directory chamada **LDAP Ping**. Ela não é uma busca normal, mas sim uma consulta que clientes fazem para descobrir a qual domínio um Controlador de Domínio pertence. Ela é usada, por exemplo, quando um computador está ingressando no domínio e precisa saber quem responder.

O detalhe crucial é que **o LDAP Ping é tratado pelo `netlogon.dll`, não pelo motor LDAP (`ntdsa.dll`)**. Como o motor LDAP nunca processa a requisição, o **Event 1644 nunca é gerado**, não importa quantos pings o atacante faça.

Ferramentas como o `ldapnomnom` abusam exatamente disso. Elas enviam LDAP Pings em massa para enumerar nomes de usuário, testando `bilbo`, `tauriel`, `thorin`, `gandalf`, sem gerar um único 1644. O rastro existe, mas está em outro lugar, no **`netlogon.log`**, que registra cada username sondado.

```
                          ┌─────────────────────────┐
   Cliente LDAP ──────────▶│  porta 389 (TCP/UDP)    │
                          └────────────┬────────────┘
                                       │
                          ┌────────────▼────────────┐
                          │     Qual motor atende?   │
                          └──┬──────────────────┬───┘
                             │                  │
                    Busca normal         LDAP Ping
                             │                  │
                             ▼                  ▼
                    ┌──────────────┐   ┌──────────────┐
                    │  ntdsa.dll   │   │ netlogon.dll │
                    │  (motor LDAP)│   │  (Netlogon)  │
                    └──────┬───────┘   └──────┬───────┘
                           │                  │
                           ▼                  ▼
                    ┌──────────────┐   ┌──────────────┐
                    │ Event 1644   │   │ netlogon.log │
                    │  (se pesado) │   │  (sempre)    │
                    └──────────────┘   └──────────────┘
```

A lição é que **"não tem 1644" não significa "não teve atividade LDAP"**, mas sim "a atividade não passou pelo motor LDAP que gera esse evento".

### Caso 3, o ADWS esconde o IP real

Desde o Windows Server 2008 R2, todo Controlador de Domínio tem um serviço chamado **ADWS** (*Active Directory Web Services*) rodando na porta 9389. Ele expõe uma interface SOAP que fala LDAP por baixo. Praticamente toda ferramenta moderna de administração do AD, incluindo o módulo PowerShell `ActiveDirectory` e ferramentas de ataque como o SOAPHound, usa o ADWS em vez de falar LDAP direto.

O problema é que o ADWS roda **dentro do próprio DC**. Quando ele recebe uma requisição do atacante e a repassa ao motor LDAP local, o motor vê a consulta vindo de `localhost` (`[::1]`). O Event 1644 é gerado, mas o campo **`Client`** mostra `[::1]` em vez do IP do atacante.

```
   Atacante                              DC
      │                                  │
      │──── SOAP :9389 ─────────────────▶│
      │                                  │
      │                          ┌───────▼────────┐
      │                          │  ADWS (SOAP)   │
      │                          └───────┬────────┘
      │                                  │
      │                          ┌───────▼────────┐
      │                          │ Motor LDAP     │
      │                          │ (vê [::1])     │
      │                          └───────┬────────┘
      │                                  │
      │                          ┌───────▼────────┐
      │                          │ Event 1644     │
      │                          │ Client: [::1]  │
      │                          └────────────────┘
```

O 1644 existe, mas a origem está mascarada. Para recuperar o IP real, é preciso correlacionar com o **Event 5156** (Windows Filtering Platform), que registra a conexão de rede verdadeira na porta 9389.

### Caso 4, a ofuscação de filtros

Existe um caso ainda mais sutil. Ferramentas como o SOAPHound constroem filtros LDAP que não fazem sentido sintático no schema do AD. Por exemplo, buscam por um atributo que **não existe**, como `(!soaphound=*)`.

O que o motor LDAP faz com isso? Ele aplica uma **otimização interna**. Como o atributo não existe, a comparação sempre resulta em falso, e a negação disso é sempre verdadeiro. O que o Event 1644 registra, então, não é o filtro original, mas a forma **normalizada** que o motor usou internamente.

```
   Filtro enviado pelo atacante:    (!soaphound=*)
   Filtro registrado no Event 1644: ( ! (FALSE) )
```

Qualquer regra Sigma que procure a string `soaphound` no log nunca vai disparar. O ataque é invisível para assinatura por string.

O mesmo acontece com variações de espaçamento (filtros equivalentes que aparecem com espaços diferentes no log) e com filtros baseados em OIDs (que aparecem como operações bitwise em vez de strings legíveis).

---

## Como amarrar os pontos

Se cada fonte tem uma cegueira, a resposta não é escolher uma fonte, mas **correlacionar**. O LDAP defensivo é um exercício de montar quebra-cabeça com peças que estão em lugares diferentes.

Aqui está o mapa de cobertura, resumido.

| Cenário | O que o 1644 vê | O que escapa | Onde procurar |
| --- | --- | --- | --- |
| Enumeração clássica (TCP 389) | Filtro normalizado, DN base, nº de entradas | Consultas pequenas diluídas | Regra estatística no próprio 1644 |
| LDAP Ping (UDP 389) | **Nada** | Tudo | `netlogon.log` |
| LDAP Ping via TCP | **Nada** | Tudo | `netlogon.log` + **Event 5156** (IP real) |
| Enumeração via ADWS (9389) | Filtro + `Client: [::1]` | IP real do atacante | **Event 5156** correlacionado ao 1644 |
| Filtros ofuscados (SOAPHound, OIDs) | Sintaxe transformada (`(!FALSE)`) | A consulta original | Estatística nos campos de performance do 1644 |

A tradução disso em prática de SOC aparece nos pontos a seguir.

**1. Não confiar em assinatura de string de filtro.** O motor LDAP reescreve filtros antes de logar. Regras que procuram por `soaphound`, `bloodhound` ou nomes específicos de ferramentas vão falhar contra adversários que ofuscam.

**2. Usar o 1644 pelo que ele é bom, a estatística.** Os campos de *número de entradas visitadas* e *tempo de processamento* não são afetados por ofuscação. Uma explosão desses valores para um IP não inventariado é um sinal forte, independente do filtro.

**3. Correlacionar o 1644 com o 5156.** Se o 1644 mostra `Client: [::1]`, o 5156 mostra o IP real que abriu a conexão na 9389. A junção dos dois reconstrói a origem.

**4. Monitorar o `netlogon.log`.** Se o 1644 está silencioso mas o `netlogon.log` mostra um bombardeio de usernames (bilbo, tauriel, thorin, gandalf...), estamos diante de um LDAP Ping enumerando usuários. O evento que "deveria" aparecer não aparece porque o caminho de código é outro.

**5. Ter visibilidade de rede como complemento.** Em ambientes pequenos, uma captura de pacotes com filtro `ldap` no Wireshark já revela a conversa crua. Em ambientes grandes, um Zeek com o parser de LDAP ligado (ou o Suricata com regras específicas) faz o mesmo em escala.

---

## Os logs são tudo, meu irmão!

Voltando ao que dissemos na introdução, há uma diferença entre olhar para um log e conseguir lê-lo. O Event ID 1644, sozinho, é uma linha. Mas quando entendemos que ele é o **eco de uma conversa** entre cliente e servidor, com um `BindRequest` ou um `SearchRequest` na origem, o log deixa de ser texto e passa a ser uma **narrativa**.

E como toda narrativa, ela pode ter buracos, com partes contadas pelo `netlogon.log`, partes escondidas atrás de um `[::1]` do ADWS, partes reescritas pelo motor LDAP antes de virarem registro. O trabalho do analista não é decorar as peças, mas saber **onde cada peça se encaixa**, e por qual caminho de código a conversa passou até virar o log que estamos lendo.

É por isso que gostamos dos bytes e das RFCs ao mesmo tempo. As RFCs contam a teoria, a intenção original de quem desenhou o protocolo. Os bytes contam a prática nua e crua, aquilo que realmente está rolando na trincheira. 

É na costura entre teoria e prática, entre o que deveria acontecer e o que de fato aconteceu, que a análise acontece.

Obrigado pela leitura até aqui, querido leitor!