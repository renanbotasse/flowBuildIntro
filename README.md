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

Falando de forma mais técnica, o FlowBuild não é executor de BPMN (Business Process Model and Notation) mas é inspirado nele como executor de processos.

Já os processos, são considerados como "uma sequencia de atividades de uma organização com o objetivo de realizar um trabalho", sendo possível linkar diretamente o processo com o desenvolvimento de software, porque esses processos são basicamente uma forma de orquestrar serviços, e a orquestração de serviços, é comumente conhecida como "microserviços".

O flowBuild se propoem a possibilitar o desenvolvimento de microserviços através de uma plataforma padrão que saiba lidar com processos, vez que, por mais complexo que sejam, processos serão sempre processos, limitado a tarefas, tempo de começo, fim, entradas e saídas. 

E por qual motivo o flowBuild é uma ferramenta que facilita a orquestração de serviços? Primeiramente porque seu objetivo é literamente facilitar a compreensão do projeto para todos os envolvidos, das mais difernetes àreas, facilitando a visualização do desenvolvimento do processo.

Por ser composto por elemento visuais e texto (Diagrama), além de código em si, permite que tanto a equipe de marketing consiga entender o que é necessário ser feito, quanto a equipe do RH e os programadores. 


- OBS: Não pode ser considerado um executor puro do BPMN, pois o BPM possui mais de 100 Elementos gráficos, já o FlowBuild possui "apenas" 8. A questão é que com "apenas" 8, é possível cobrir quase 95% das utilidades do BPMN, assim, diminuir em 92% as possibilidades de Elementos torna muitíssimo mais fácil a compreensão do projeto, sem quase nenhuma perda de qualidade por isso. Além disso, em vez de utilizar XML, utilizamos JSON, tornando mais flexível, fácil de ler e mais leve de transportar. Em resumo, pode ser considerado uma versão mais simples, mais fácil de utilizar, portanto, mais efetiva. 

### REPRESENTAÇÃO GRÁFICA NO FLOWBUILD (QUATRO TIPOS DE NÓS)

1. EVENTS (Timer):
  * START: Inicio do processo.
  * FINISH: O processo foi encerrado. Informar em qual momento houve o encerramento.

2. TASKS:
  * USERTASK: Tarefas que precisam de interação com o usuário. Lembrar que o input são como os parametros que devem ser recebidos pelo usuário para poder realizar.
  * SYSTEMTASK: São as tarefas do sistema, não precisa do usuário para ser realizada. Não há problema em ser um pouco mais verboso no name (!id). As tarefas do sistema podem ter várias categorias, as mais utilizadas são o HTTP (API: GET, POST, e etc). 
 * SUBPROCESS: Quando um processo fica grande demais, ele pode ser dividido em subprocessos e utilizar os próprios subprocessos.

3. GATEWAY: Envia o processo para outra etapa. Precisa de ter mais de um NEXT (OK e NOT OK), qual o DEFAULT também. 

4. LANE: É o controle de acesso a um conjunto de nós. Feito para separar a responsabilidades de cada tarefa. 
 * SWIMLANE: Dividir as linhas de interação entre as pessoas que tem acesso ao sistema, até onde o usuário-cliente pode interagir ou onde cliente-pizzaria pode agir. Esse é um dos principais pontos, vez que se pessoas não autorizadas terem acesso a funcionalidades que não são de seu grupo, pode comprometer o projeto.
 
 * ATORES: É importante deixar claro quem é que vai realizar cada tarefa, se será o usuário (no nosso caso: cliente da pizzaria ou a própria pizzaria) ou o próprio sistema. 


## JSON
Blueprint é um item que descreve o processo para a interpretação do Flowbuild. É um JSON passível de interpretação pelo FlowBuild.

Para armazenar uma blueprint são necessárias três informações:

* name: Nome da blueprint (evitar o uso de espaços e caracteres especiais).

* description: Descrição da blueprint.

* blueprint_spec: Esquema de execução que será utilizado pelo FlowBuild.

### A blueprint é definida por um Objeto com 6 atributos:

* prepare: Lista de funções que devem ser executadas antes da inicialização do processo.

* requirements: Lista de packages que devem ser importados.

* enviroment: Deve trazer para a blueprint as variáveis de ambiente da aplicação (EX: Atribui o valor da env API_KEY com o nome X-API-KEY).

* parameters: Um Objeto onde são definidas as constantes aplicadas naquela determinada blueprint.

* lanes: É o controle de acesso a um conjunto de nós. Define quais regras devem ser atendidas para que um usuário tenha acesso a um determinado nó.

* nodes: Um nó é a menor unidade do processo, é uma tarefa que deve ser executada.

### NODES

O que é necessário para a existência dos nodes:

* id: Definido como uma string, é o identificador do nó e deve ser único no contexto da blueprint;

* name: Nome do nó, tem uma função descritiva para o usuário que lê a blueprint. Não afeta a execução do processo, porém detém muito valor para análise futura e rastreamento;

* lane_id: Uma string que faz referência ao id de umas das lanes da blueprint. Uma falha na referência impede a blueprint de ser publicada.

* next: Indica qual o próximo nó será executado após a execução do nó atual. Deve fazer referência a um nó da própria blueprint. A inexistência de referência impede a blueprint de ser publicada.

* type: Define o tipo de tarefa que deverá ser realizada. Veja a seção de nodeTypes para mais detalhes.

* category: Atributo exclusivo para systemTaskNodes.

* parameters: É definido por um objeto com os parâmetros de execução do nó e dados de input (quando aplicável).


### startNode

* input_schema: Um objeto representando o JSON Schema do payload de inicio do processo.
* timeout: Um número inteiro que representa o prazo (em segundos) para expiração do processo. 

```
{
    "id": "string",
    "name": "string",
    "next": "string",
    "type": "start",
    "lane_id": "string",
    "parameters": {
        "input_schema": {},
        "timeout": 100
    }
}
```

### finishNode

* next: deve ser null. Também pode receber parâmetros opcionais.

* parâmetros do finishNode transferem os dados para o campo result no final do processo.

Caso o processo seja evocado como um subProcesso, os result do finishNode será transmitido para o processo-pai.

```
{
  "id": "any_string (system friendly recommended)",
  "name": "any string",
  "type": "Finish",
  "lane_id": "any_lane_id",
  "next": null
}
```

### flowNode

Em seus parâmentros um único atributo será utilizado para direcionar o processo.

O valor atribuído será convertido em texto e comparado com as opções descritas no objeto next descrito no especificação do nó.

Caso o atributo especificado nos parameters não esteja definido, o flowNode gerará o texto undefined para comparação.

Diferente dos demais nós do flowBuild, o atributo next de um flowNode é representado por um objeto e não por uma string.

Este objeto deve ser um conjunto de atributos que serão avaliados contra o valor do parâmetro especificado.

É obrigatório que um dos atributos do objeto next do flowNode seja default, que será utilizado caso nenhum resultado seja identificado.

```
{
  "id": "any_string ",
  "name": "any string",
  "next": {
    "string": "other_node_id",
    "default": "other_node_id"
  },
  "type": "flow",
  "lane_id": "any_lane_id",
  "parameters": {
    "input": {
      "key": "string"
    }
  }
}
```

### userTaskNode

Este tipo de nó descreve uma interação, normalmente com um humano.

O processo ao atingir um nó de userTask, realiza uma pré-execução, que avaliará os parâmetros de entrada da tarefa e enviará tais parâmetros para o gerenciador de atividades (Activity Manager).

Diferente das tarefas de sistema, um userTask gera uma interrupção do processo, que entra em um estado de espera WAITING até que receba uma confirmação do Activity Manager de que a tarefa foi concluída. Dessa forma, assim como o startNode, uma userTask gera 2 estados no processo.

Uma userTask pode receber até 6 parâmetros:

* action (obrigatório)

* input (obrigatório)

* timeout

* activity_schema

* activity_manager

* result_schema

```
{
  "id": "any_string (system friendly recommended)",
  "name": "any string",
  "next": "other_node_id",
  "lane_id": "any_lane_id",
  "type": "UserTask",
  "parameters": {
    "action": "ANY_STRING_HERE",
    "input": {},
    "activity_manager": "commit or notify",
    "activity_schema": {"$ref": "activity_schema"},
    "timeout": 60
  },
  "result_schema": {}
}
```

### systemTaskNode
O systemTaskNode espera um atributo adicional que descreve a categoria da tarefa a ser realizada, entre elas:

* HTTP
````{
  "id": "any_string (system friendly recommended)",
  "name": "any string",
  "next": "other_node_id",
  "lane_id": "one_lane_id",
  "type": "SystemTask",
  "category": "http",
  "parameters":  {
    "input": {},
    "request": {
      "url": "url",
      "verb": "GET,POST,PUT,PATCH,DELETE",
      "headers": {}
    }
  },
  "result_schema": {}
}
```

* SetToBag
```
{
  "id": "any_string (system friendly recommended)",
  "name": "any string",
  "next": "other_node_id",
  "lane_id": "one_lane_id",
  "type": "SystemTask",
  "category": "setToBag",
  "parameters": {
    "input": {}
  }
}
```

### subprocessNode
Este nó pode receber 4 parâmetros:

* workflow_name (obrigatório)

* actor_data (obrigatório)

* input

* valid_response

```
{
  "id": "any_string (system friendly recommended)",
  "name": "any string",
  "type": "SubProcess",
  "lane_id": "any_lane_id",
  "next": "other_node_id"
  "parameters":{
     "workflow_name": "string",
     "actor_data": {"$ref": "actor_data"},
     "valid_response":{},
     "input":{}
  }
}
```


## RESOLUÇÃO

## FEATURES (O QUE ACHO IMPORTANTE TER)

### ESSENCIAIS

### IMPORTANTES

### RETIREI

## FIM FETAURES QUE PODERIAM TER (NÃO IMPLEMENTEI PQ IRIA FICAR GRANDE DEMAIS E NÃO SERIA TÃO ÚTIL QUANTO AS OTURAS QUE JÁ ADICIONEI)
