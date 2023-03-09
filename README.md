# PROCESSO SELETIVO FDTE

## INTRODUÇÃO

O processo seletivo da Fundação para o Desenvolvimento Tecnológico da Engenharia (FDTE) para a vaga Treainee (na vertical de workflow) é composto por um desafio a ser realizado no em 7 (sete) dias, devendo ser entregue: Diagrama, BluePrint e Apresentação.

O desafio será avaliado pelo time que trabalha diretamente com o workflow.

## DESAFIO

O Desafio consiste em propor um processo de entrega de pedido de pizza a ser implementado por uma empresa de delivery de pizza.

Como é um processo de pedido de pizza, não é necessário literalmente projetar o aplicativo e sim fazer o diagrama e a bluprient.

O blueprint é basicamente um arquivo JSON que respeita a formatação do flowBuild.

O blueprint deve ser executável dentro do servidor disponibilizado pela Fundação, até mesmo para facilitar a compreensão dos avaliadores do que foi produzido.

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

Para aprimorar o projeto base, consultei alguns aplicativos de delivery como: [iFood](https://www.ifood.com.br/?toHome=true), [PlusDelivery](https://www.plusdelivery.com.br/), [telepizza](https://www.telepizza.pt/) e [Domino's](https://www.dominospizza.pt/).

Junto com a análise crítica desses aplicatívos, dei ênfase na minha experiência como usuário e discussões que já tive com amigos sobre o que os aplicativos deveriam aprimorar. 

## FLOWBUILD

Antes de propriamente iniciar a explicação da resolução para o desafio, é necessário falar sobre a ferramente a ser utilizada, o FlowBuild.

De forma extremamente básica, o FlowBuild pode ser compreendido como "uma biblioteca utilizada para criar soluções", uma plataforma para criar processos.

Falando de forma mais técnica, o FlowBuild não é executor de BPMN (Business Process Model and Notation) mas é inspirado nele como executor de processos.

Já os processos, são considerados como "uma sequencia de atividades de uma organização com o objetivo de realizar um trabalho", sendo possível linkar diretamente o processo com o desenvolvimento de software, porque esses processos são basicamente uma forma de orquestrar serviços.

O FlowBuild se propoem a possibilitar o desenvolvimento de microserviços através de uma plataforma padrão que saiba lidar com processos, vez que, por mais complexo que sejam, processos serão sempre processos, limitado a tarefas, tempo de começo, fim, entradas e saídas. 

E por qual motivo o FlowBuild é uma ferramenta que facilita a orquestração de serviços? Primeiramente porque seu objetivo é literamente facilitar a compreensão do projeto para todos os envolvidos, das mais diferentes àreas, facilitando a visualização do desenvolvimento do processo.

Por ser composto por elemento visuais e de texto, além do código em si, permite que todos os setores envolvidos no desenvolvimento do produto consigam entender o que o produto precisa para ser implementado e facilita a divisão de tarefas na construção do mesmo, sendo útil até mesmo na manutenção do produto.


- OBS: O FlowBuild não pode ser considerado um executor puro do BPMN, pois o BPM possui mais de 100 Elementos gráficos, já o FlowBuild possui "apenas" 8. A questão é que com "apenas" 8, é possível cobrir quase 95% das utilidades do BPMN, assim, diminuir em 92% as possibilidades de elementos torna muitíssimo mais fácil a compreensão do projeto, sem quase nenhuma perda de qualidade por isso. Além disso, em vez de utilizar XML, utiliza JSON, tornando mais flexível, fácil de ler e mais leve de transportar. Em resumo, pode ser considerado uma versão mais simples, mais fácil de utilizar, portanto, mais efetiva. 

### REPRESENTAÇÃO GRÁFICA NO FLOWBUILD (QUATRO ELEMENTOS)

1. EVENTS:
  * START: Inicio do processo.
  * FINISH: O processo foi encerrado. Informar em qual momento houve o encerramento.

2. TASKS:
  * USERTASK: Tarefas que precisam de interação com o usuário. Lembrar que o input são como os parametros que devem ser recebidos pelo usuário para poder realizar.
  * SYSTEMTASK: São as tarefas do sistema, não precisa do usuário para ser realizada. Não há problema em ser um pouco mais verboso no name (!id). As tarefas do sistema podem ter várias categorias, as mais utilizadas são o HTTP (POST, GET, PUT, PATCH, DELETE e HEAD). 
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

* name: Nome do nó, tem uma função descritiva para o usuário que lê a blueprint.

* lane_id: Uma string que faz referência ao id de umas das lanes da blueprint.

* next: Indica qual o próximo nó será executado após a execução do nó atual.

* type: Define o tipo de tarefa que deverá ser realizada.

* category: Atributo exclusivo para systemTaskNodes.

* parameters: É definido por um objeto com os parâmetros de execução do nó e dados de input.


### startNode

* input_schema: Um objeto JSON usando para carregar informações que serão usadas durante o processo.
* timeout: prazo para expiração do processo. 

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

Se estiver dentro de um subProcesso, os result do finishNode será transmitido para o processo-pai.

Como o FlowBuild é baseado em serialismo (um sentido só), mesmo dentro de subProcessos, eles devem ser concluído para o processo principal continuar. FlowBuild não aceita paralelismo.

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

O valor atribuído será convertido em texto e comparado com as opções descritas no objeto next (True ou False. Default no True).

Diferente dos demais nós do flowBuild, o atributo next de um flowNode é representado por um objeto e não por uma string.

Este objeto deve ser um conjunto de atributos que serão avaliados contra o valor do parâmetro especificado.

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
```
{
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

Para o desafio ele não é tão interessante pois precisa de um conhecimento um pouco mais aprofundado e mais prática com o FlowBuild para utilizar sem nenhum tipo de erro.

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

****

# APRESENTAÇÃO

***

1. [BASE](#base)
2. [SOLUÇÃO](#solucao) 
 	- 2.1 [Permitir edição e comentário pelo Cliente](#edicao) 
	- 2.2 [Permitir cancelamento pela Pizzaria](#cancelamento) 
 	- 2.3 [Evitar errors pela Pizzaria](#erros) 
 	- 2.4 [Evitar impressão negativa - Cupom de desconto](#cupom)  
 	- 2.5 [Evitar prejuízo (Cliente não encontrado)](#prejuizo) 
3. [DIFICULDADES E IDEIAS NÃO APLICADAS](#dificuldades)
	- 3.1. [Cliente ter atualização do status do pedido](#status) 
	- 3.2. [Cancelamento pelo Cliente](#cancelamentoc) 
	- 3.3. [Otimizador de Entrega (SubProcesso)](#otimizador)  
	- 3.4. [Retirada do Elogio/Reclamação](#elogio_reclamação)
	- 3.5. [Conectar Diagrama com JSON](#json) 
	- 3.6. [Inputs e SystemNode (HTTPS)](#https) 
	- 3.7. [Envitar confusão no processo](#confusao) 
4. [CONCLUSÃO](#conclusao)

## 1. BASE <a name="base"></a>

O Desafio consiste em propor um processo de entrega de pedido de pizza a ser implementado por uma empresa de delivery de pizza. Sendo entregue o diagrama abaixo para ser melhorado.

<img width="100%" alt="Screenshot 2023-03-09 at 12 16 47" src="https://user-images.githubusercontent.com/101360239/224020626-eb0871f5-a338-4eb8-b44c-5150f8e02697.png">

## 2. SOLUÇÃO <a name="solucao"></a>

A minha solução para o Desafio é a seguinte:

![renanb (6)](https://user-images.githubusercontent.com/101360239/224022944-102ba1fa-7e37-4156-afad-09aac2a2d527.png)

2.1. Permitir edição e comentário pelo Cliente <a name="edicao"></a>

<div align="center">
	
<img width="450" height="300" align="center" alt="Screenshot 2023-03-09 at 12 26 03" src="https://user-images.githubusercontent.com/101360239/224022618-a40cd5b2-3d7b-4239-bbbc-75291766a725.png">

</div>

	
2.2. Permitir cancelamento pela Pizzaria <a name="cancelamento"></a>


+ reembolso
+ aviso ao cliente

<div align="center">

<img width="219" alt="Screenshot 2023-03-09 at 12 27 35" src="https://user-images.githubusercontent.com/101360239/224023061-78cca8d6-786f-4b13-afcd-f806bed5dcfd.png">

</div>	
	
2.3. Evitar errors pela Pizzaria <a name="erros"></a>

<div align="center">

<img width="870" alt="Screenshot 2023-03-09 at 12 28 12" src="https://user-images.githubusercontent.com/101360239/224023218-7573f4c0-c043-4fdf-a78c-2207779de122.png">

</div>

+ Cliente revisa
+ Recebe pedido com tempo real e dilatado
+ Pode não aceitar
+ Monitoramento da pizzaria (acidente, luz, ingredientes)
+ Cancelar
+ Revisar pedido na pizzaria
+ Cliente revisa na entrega
+ Atraso gera desconto futuro

<div align="center">

<img width="870" alt="Screenshot 2023-03-09 at 12 28 12" src="https://user-images.githubusercontent.com/101360239/224023218-7573f4c0-c043-4fdf-a78c-2207779de122.png">

</div>
	
2.4. Evitar impressão negativa - Cupom de desconto <a name="cupom"></a>

+ Tempo dilatado
+ Tempo Real
+ Horário de Chegada (entrega)
+ Verifica tempo
+ gera cupom
+ Comunica cupom
+ Antes de pagar pode usar cupom


<div align="center">

<img width="452" alt="Screenshot 2023-03-09 at 12 29 28" src="https://user-images.githubusercontent.com/101360239/224023482-c0cf39e7-87b3-439c-af81-646e07758ec7.png">

</div>
	
2.5 Evitar prejuízo (Cliente não encontrado) <a name="prejuizo"></a>

+ Pedido feito após o pagamento
+ Comprovante de pagamento
+ Cliente dá dados e revisa
+ Entregador tenta contato 2 vezes, prazo de 5 min
+ Registra tentativa
+ Volta a pizzaria
+ 

	
<div align="center">

<img width="670" alt="Screenshot 2023-03-09 at 12 31 22" src="https://user-images.githubusercontent.com/101360239/224023868-09308dd0-7a01-4182-afae-56b1d66f7b1c.png">

</div>
	
### 3. DIFICULDADES E IDEIAS NÃO APLICADAS  <a name="dificuldades"></a>

3.1. Cliente ter atualização do status do pedido<a name="status"></a>

<div align="center">

<img width="613" alt="Screenshot 2023-03-09 at 12 34 30" src="https://user-images.githubusercontent.com/101360239/224024629-ebbe0973-5881-4560-98f5-b144ab4c45d4.png">

</div>
	
Loop

Paralelismo/Serialismo

3.2. Cancelamento pelo Cliente <a name="cancelamentoc"></a>

Paralelismo/Serialismo

3.3. Otimizador de Entrega (SubProcesso)<a name="otimizador"></a>

Mais que um pedido, inúmeros nós ao final. Ficaria complexo demais para o que foi proposto.

<div align="center">

<img width="623" alt="Screenshot 2023-03-09 at 12 47 36" src="https://user-images.githubusercontent.com/101360239/224027491-d7244102-903e-456e-a934-dba4686350fb.png">

</div>

<div align="center">

<img width="1087" alt="Screenshot 2023-03-09 at 14 23 24" src="https://user-images.githubusercontent.com/101360239/224054051-aeff82a6-da8a-4780-bc22-aa22c2502f38.png">

</div>
	
3.4. Retirada do Elogio/Reclamação <a name="elogio_reclamação"></a>

Substitui pelo Cupom - Acho mais efetivo

3.5. Conectar Diagrama com JSON <a name="json"></a>

3.6. Inputs e SystemNode (HTTPS)<a name="https"></a>

<div align="center">

<img width="50%" alt="Screenshot 2023-03-09 at 14 12 23" src="https://user-images.githubusercontent.com/101360239/224051237-7d81d7ef-d1ec-4acc-b041-ba964982dc6c.png">

</div>
	
3.7 Envitar confusão no processo<a name="confusao"></a>

<div align="center">

<img width="50%" alt="Screenshot 2023-03-09 at 12 45 10" src="https://user-images.githubusercontent.com/101360239/224026856-6856f2c7-04f0-487c-9831-c868209a1155.png">

</div>
	
## 4. CONCLUSÃO <a name="conclusao"></a>

Diagramas e Nós são boas formas de organizar
Lanes e permissões dão segurança
Gateways dão opções e evita problemas já que é serialismo.
