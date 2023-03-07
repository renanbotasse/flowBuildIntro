# PROCESSO SELETIVO FDTE

## INTRODUÇÃO

O processo seletivo da Fundação para o Desenvolvimento Tecnológico da Engenharia (FDTE) para a vaga Treainee (na vertical de workflow) é composto por um desafio a ser realizado no em 7 (sete) dias, devendo ser entregue: Diagrama, BluePrint e Apresentação.

O desafio será avaliado pelo time que trabalha diretamente com o workflow.

## DESAFIO

O Desafio consiste em propor um processo de pedido de pizza, como se estivesse atendendo uma empresa de delivery de pizza.

Como é um processo de pedido de pizza, não é necessário literalmente projetar o aplicativo e sim fazer o workflow (Diagrama) do funcionamento do aplicativo.

Outro ponto a ser salientado é a necessidade da utilização do BluePrint, um arquivo JSON, que respeita a formatação do flowBuild.

O BluePrint deve ser executável dentro do servidor disponibilizado pela Fundação, até mesmo para facilitar a compreensão dos avaliadores do que foi produzido.

A explicação não deve se limitar a explicar o fluxo e o código, deve incluir as ponderações sobre o que mais gostou, menos gostou, quais foram as decisões que precisou tomar e porque tomou essas decisões, quais foram as soluções adotadas e sua motivação.

## MATÉRIA BASE

A Fundação disponibiliza um bom material base para a realização do projeto.

- 1 - Canal no Slack para tirar dúvidas;

- 2 - Servidor próprio para testar o projeto;

- 3 - Indicação de ferramenta para criar o [Diagrama](www.cawemo.com);

- 4 - Documentação do [FlowBuild](https://flow-build.github.io/) com vários detalhes sobre formatação e exemplos;

- 5 - Projeto Base a ser melhorado:
![image](https://user-images.githubusercontent.com/101360239/223406220-017fd98d-35f3-4448-a9bd-de3cb0b3fbff.png)

- 6 - Slides com a descrição dos Elementos;

## INSPIRAÇÕES

Para aprimorar o projeto base, consultei alguns aplicativos de delivery de comida como: [iFood](https://www.ifood.com.br/?toHome=true), [PlusDelivery](https://www.plusdelivery.com.br/), [telepizza](https://www.telepizza.pt/) e [Domino's](https://www.dominospizza.pt/).

Junto com a análise crítica desses aplicatívos, dei enfase na minha experiência como usuário e discussões que já tive com amigos sobre o que os aplicativos poderiam aprimorar ou quais são os pontos mais fortes deles. 

## FLOWBUILD

Antes de propriamente iniciar a explicação da minha resolução para o desafio, é necessário falar sobre a ferramente a ser utilizada, o FlowBuild.

De forma extremamente básica, o FlowBuild pode ser compreendido como "uma biblioteca em que soluções são criadas através dela", uma plataforma para criar processos.

Falando de forma mais técnica, o FlowBuild é um tipo de executor (não puro) de BPMN (Business Process Model and Notation), ou seja, um executor de anotações de descrição de processos.

Já os processos, são considerados como "uma sequencia de atividades de uma organização com o objetivo de realizar um trabalho", sendo possível linkar diretamente o processo com o desenvolvimento de software, porque esses processos são basicamente uma forma de orquestrar serviços, e a orquestração de serviços, é comumente conhecida como "microserviços".

O flowBuild se propoem a possibilitar o desenvolvimento de microserviços através de uma plataforma padrão que saiba lidar com processos, vez que, por mais complexo que sejam, processos serão sempre processos, limitado a tarefas, tempo de começo, fim, entradas e saídas. 

E por qual motivo o flowBuild é uma ferramenta que facilita a orquestração de serviços? Primeiramente porque seu objetivo é literamente facilitar a compreensão do projeto para todos os envolvidos, das mais difernetes àreas, facilitando a visualização do desenvolvimento do processo.

Por ser composto por elemento visuais e texto (Diagrama), além de código em si, permite que tanto a equipe de marketing consiga entender o que é necessário ser feito, quanto a equipe do RH e os programadores. 


- OBS: Não pode ser considerado um executor puro do BPMN, pois o BPM possui mais de 100 Elementos gráficos, já o FlowBuild possui "apenas" 8. A questão é que com "apenas" 8, é possível cobrir quase 95% das utilidades do BPMN, assim, diminuir em 92% as possibilidades de Elementos torna muitíssimo mais fácil a compreensão do projeto, sem quase nenhuma perda de qualidade por isso. Além disso, em vez de utilizar XML, utilizamos JSON, tornando mais flexível, fácil de ler e mais leve de transportar. Em resumo, pode ser considerado uma versão mais simples, mais fácil de utilizar, portanto, mais efetiva. 

### REPRESENTAÇÃO GRÁFICA NO FLOWBUILD (CINCO TIPOS DE NÓS)

- START: Inicio do processo.

- USERTASK: Tarefas que precisam de interação com o usuário. Lembrar que o input são como os parametros que devem ser recebidos pelo usuário para poder realizar.

- SYSTEMTASK: São as tarefas do sistema, não precisa do usuário para ser realizada. Não há problema em ser um pouco mais verboso no name (!id). As tarefas do sistema podem ter várias categorias, as mais utilizadas são o HTTP (API: GET, POST, e etc). 

- GATE: Envia o processo para outra etapa. Precisa de ter mais de um NEXT (OK e NOT OK), qual o DEFAULT também. 

- END: O processo foi encerrado. Informar em qual momento houve o encerramento.
 
     - SWIMLANE: Dividir as linhas de interação entre as pessoas que tem acesso ao sistema, até onde o usuário-cliente pode interagir ou onde cliente-pizzaria pode agir. Esse é um dos principais pontos, vez que se pessoas não autorizadas terem acesso a funcionalidades que não são de seu grupo, pode comprometer o projeto.

     - ATORES: É importante deixar claro quem é que vai realizar cada tarefa, se será o usuário (no nosso caso: cliente da pizzaria ou a própria pizzaria) ou o próprio sistema. 

## RESOLUÇÃO

## FEATURES (O QUE ACHO IMPORTANTE TER)

### ESSENCIAIS

### IMPORTANTES

### RETIREI



## FIM FETAURES QUE PODERIAM TER (NÃO IMPLEMENTEI PQ IRIA FICAR GRANDE DEMAIS E NÃO SERIA TÃO ÚTIL QUANTO AS OTURAS QUE JÁ ADICIONEI)
