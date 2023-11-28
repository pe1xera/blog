+++
title = 'Minha experiência com a certificação PJPT'
date = 2023-11-20
cover = "pjpt-capa.png"
+++

# Introdução

No dia 25 de Agosto de 2023, completei a "prova" da certificação PJPT, da TCM Security.

De acordo com o site oficial, "a certificação **Practical Junior Penetration Tester™ (PJPT)** é uma experiência de pentest de nível iniciante. Este exame avaliará a capacidade do aluno de realizar um teste em uma rede interna a nível de associado. Os alunos terão dois (2) dias completos para concluir a avaliação e mais dois (2) dias adicionais para escrever um relatório profissional.

Para receber a certificação, o aluno deve:

**1)** Utilizar suas habilidades de exploração do Active Directory para realizar movimentos laterais e verticais na rede e, por fim, comprometer o Controlador de Domínio (DC) do exame.  
**2)** Fornecer um relatório detalhado e profissionalmente escrito."

Atualmente, a certificação custa $199.00 (199 dólares). Por se tratar de uma transferência internacional, foram acrescidos impostos e o valor ficou em $214.00 (por volta de R$ 1100.00). Francamente, achei um valor bem justo pela densidade do material do curso, especialmente quando comparado a outras certificações de mesmo nível.  
Vale lembrar que o valor já inclui o treinamento e uma segunda tentativa grátis. 

---
# O treinamento

A própria TCM Security oferece um curso chamado Practical Ethical Hacking, ou PEH, como preparação para sua certificação. Apesar do nome, o curso não pretende ser um "Canivete Suiço" que ensine tudo sobre segurança ofensiva.

Ainda assim, sem sombra de dúvidas, este é um dos melhores cursos que já tive a oportunidade de completar. É realmente prático. O tipo de material que expande completamente os horizontes, mesmo de quem já tem um certo entendimento de Segurança da Informação e Hacking.

O foco no mindset é um diferencial. Não espere um curso que te recheia de ferramentas - que podem mudar ou ficarem obsoletas até mesmo enquanto escrevo esse texto. Muito pelo contrário!

No curso temos, dentre outros:
- Forte foco no processo de enumeração;
- Pentest em AD e diversos vetores de ataque;
- Revisão dos ataques mais comuns por Web Hacking;
- Dicas e insights na escrita de relatórios.

As 25 horas de material se multiplicaram até ocuparem um mês inteiro, no qual pude construir o laboratório, praticar nos desafios e fazer anotações estratégicas.

Como bônus, o suporte do curso via Discord é absolutamente fantástico. Existe todo um ecossistema da comunidade TCM no Discord, que se propõe a ajudar os alunos em suas dúvidas e sanar os possíveis gaps. Além disso, o curso é atualizado com frequência e recebeu, recentemente, um módulo web totalmente repaginado com challenges práticos.

{{< image src="../../../pjpt-web.png" >}}  

---
# Preparação

Se posso dar alguma dica é: **Estude de verdade, meu caro**.

Faça todos os labs, construa o ambiente virtual conforme é orientado durante o curso e faça os testes. Sem essa experiência hands-on (e as dores de cabeça para consertar os problemas no meu lab), eu certamente não teria passado na prova.

Fiz todas as anotações via Notion, pela praticidade e familiaridade que já tenho com a ferramenta. Com anotações, quero dizer comandos, dicas do professor, assim como prints da construção (e desastres) dos labs. Novamente, esse processo fez toda a diferença.

{{< image src="../../../lab-pjpt.png" >}}   

Não adianta tentar tapar o sol com a peneira ou pular etapas do treinamento para finalizá-lo logo. A única forma de passar na prova é compreendendo **BEM** tudo aquilo que foi ensinado pelos professores (Heath Adams e Alex Olsen). 

Não se engane pelo 'J' de Junior. Trata-se de uma prova prática, então decorar conceitos prontos ou apenas assistir as aulas não irão te levar a lugar algum. É preciso saber fazer, na prática, um pentest em rede interna, levando em consideração aquilo que que se aprende no treinamento.

---
# O Grande Dia!

>Falando especificamente da prova, dei início à tentativa às 08:10 do dia 24/08.  

A vontade de pegar o Domain Admin é grande, mas a primeira coisa a se fazer é assinar um Non-Disclosure Agreement, exatamente como em um pentest real, o que dá um ar de seriedade à certificação, pois se compromete a simular um ambiente realístico, sem flags ou questões de múltipla escolha. Pois bem. 

Durante as primeiras horas, eu estava nervoso, por essa ser primeira primeira certificação prática. Fui apenas me ambientando, no primeiro momento, e fazendo o processo de Reconhecimento na rede. Não posso dar muitos detalhes - do contrário estaria quebrando os termos de confidencialidade -, mas quem quer que faça o curso, os laboratórios e entenda o que está fazendo no processo de condução do pentest com certeza se sairá bem.

{{< image src="../../../pjpt-etapas.png" >}}  

Em determinado momento da tarde, me senti travado e não sabia mais como prosseguir. Nada de domain admin nem credenciais úteis para movimentação vertical ou lateral. Frustração enorme. Algumas ferramentas se demonstraram inúteis durante o processo, à medida que eu tentava seguir caminhos que não foram ensinados durante o curso - grande erro.

Neste momento, decidi dar uma pausa e desprender completamente meu pensamento da certificação e do ambiente. Levantei e fui conversar com a família, para rir um pouco, espairecer e tentar reorganizar as ideias, sendo essa a melhor decisão que tomei.

Quando voltei ao exame, lembrei dos problemas que tinha enfrentado antes e pressupus que esse não era o caminho. Tentei, então, uma outra abordagem com base naquilo que aprendi durante o curso, mas adaptada para o cenário em que eu estava. Consegui algumas credenciais e um norte de como chegar até o sonhado Domain Controller.

Fui dormir tranquilamente, pois já estava mais confiante de que conseguiria completar o exame, desde que administrasse bem o tempo.   
No dia seguinte (25/08), por volta das 10:20, **BOOM! CONSEGUI O DOMAIN ADMIN!**

A partir daí, completei as tarefas restantes e dei uma boa olhada no ambiente, antes de finalizar a tentativa pelo sistema da TCM. É importante ir tirando prints durante o processo, para documentar o pentest e inserir no relatório, o ápice da certificação.

---

# Pós-Exame

O período de confecção do report foi extremamente divertido. Nele, é necessário categorizar as vulnerabilidades encontradas com base no CVSS, assim como recomendar as remediações para correção delas no ambiente. O objetivo é que os avaliadores consigam chegar ao mesmo resultado que o tester seguindo seus passos e lógica.

Pouco após submeter o report no sistema e finalizar, de vez, a tentativa, um dos moderadores do Discord informou que estava lendo o meu documento. HYPE!

{{< image src="../../../pjpt-disc.png" >}}   

Novamente, ressalto a importância da comunidade no Discord e o apoio do time de suporte da TCM, que foram como verdadeiros mentores durante a minha jornada. Pouco tempo depois da análise do PDF, recebi a informação de que, sim, passei na prova de certificação e era o mais novo PJPT.   

**Vitória!**   

---
Muito obrigado pela sua leitura até aqui, querido leitor.  
Fique com a imagem da belíssima certificação.

{{< image src="../../../pjpt-cert.png" >}} 

