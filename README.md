# FlowBuild

Introdução a utilização do [FlowBuild](https://flow-build.github.io)

TAREFA - TRAINEE 
VERTICAL DE WORKFLOW (TREINAMENTO EM UMA DAS ÁREAS DE ATUAÇÃO DA FUNDAÇÃO - DESENVOLVIMENTO DE SOFTWARE ATRAVÉS DE PROCESSOS)
-> FLOWBUILD

BPMN (DEFINIÇÕES E ELEMENTOS)

CLIENTE - UMA SOLUÇÃO ESPECÍFICA - IDEIA DE FAZER 

> IR E DESONVOLVER UMA SOLUÇÃO PARA O CLIENTE <

CONSTRUIR UMA BIBLIOTECA E CRIAR UMA SOLUÇÃO ATRAVÉS DESSA BIBLIOTECA

ESSA BIBLIOTECA É OS > FLOWBUILD (UM EXECUTOR DE BPMN)

CRIOU UMA FORMA DE TRABALHO DIFERENTE ATRAVÉS DO FLOWBUILD "UM FRAMEWORK NÃO FUNCIONAL". 


FLOWBUILD É UM EXECUTOR DE BPMN

Processo é uma sequencia de atividades em uma organização com o objetivo de realizar um trabalho

no ambiente web processos pode ser defenido como a orquestração de serviços

processo é o a ordem definida de tareffas realizads em um espaço de tempo com começo, fim, entradas e saidas bem definidas


#microserviços - orquestração de serviços
#Alguem para orquestrar, organizar os serviços -> precisa criar um processo -> pq não desenvolver totalmente em baseado em sistema de orquestração (flowbuild)

BPMN (BUSINESS PROCESS MODEL AND NOTATION)
Uma forma de escrever processos (uma anotação para descrever processos)
[bolinhas quadradinhos losangolos]
portras tinha um XML que descrevia essas bolinhas quadrados e losangolos

A ideia seria pegar algo que traduz o XML pela máquina


tentativa de fazer algo grafico e visual para facilitar a compreensão do processo

QUADRADO - TERMO GENERICO PARA UM TRABALHO QUE É EXECUTADO EM UM PROCESSO (UMA TAREFA QUE TEM QUE SER EXECUTADA) - INTEGRAÇÃO COM PARCEIRO - CHAMADA DE API - UMA FUNÇÃO QUE TEM QUE SER EXECUTADA-

BOLINHAS (EVENTOS) - COISAS QUE ACONTECEM DURANTE O PROCESSO - INICIAR O PROCESSO PODE SER UM EVENTO, TERMINAR TAMBÉM, 
BOLINHA MAIS FINA - INICIO
UMA BOLINHA DENTRO DA OUTRA - INTERMEDIÁRIO
UMA BOLINHA COM BORDA GROSSA - TERMINO

LOSANGOLO (DIVISÃO DOS PROCESSOS) - PROCESSOS PONTO DE DECISÃO, EM FRENTE (PORTAIS - GATEWAYS)

SWIMINLANE - QUEM EXECUTA ESSE PROCESSO


FLOWBUILD não é um executor de BPMN puro
O formato não é o mesmo, usa JSON ao invés de XML (em vez, não)
XML é mais travado - JSON é mais flexivel e fácil de ler (mais leve para transportar)
BPMN TEM MAIS DE 100 PROCESSOS DISTINTOS
FLOWBUILD USA:
EVENTS: START FINISH TIMER
GATEWAY: FLOW (SEMPREFAZ UM)
TASK: SYSTEMTASK (TAREFA DE SISTEMA, SISTEMA QUE FAZ, UMA FUNÇÃO, API ALGO ASSIM) USERTASK (USUÁRIO - ENCAMINHADA PARA UMA FRONTEND PARA SER EXECUTADA) SUBPROCESSO (EXECUTADO PELO PRÓPRIO FLOWBUILD - EX: UM PROCESSO GRANDE DEMAIS, DIVIDE ELE E SAO CHAMADOS)
LANE: QUEM PODE FAZER O QUE

Os outros 92 são ignorados, pq o que pode ser feito com 8 tipos de elementos, dá pra cobrir 90, 95% dos Elementes (não consigo fazer paralesismo, mas dá para resolver sem isso)

uma versão mais simples e mais fácil



#DESAFIO - PIZZA
propor um processo de pedido de pizza online (uma aplicação para atender uma empresa de delivery de pizza)


![Screenshot 2023-03-06 at 21 29 09](https://user-images.githubusercontent.com/101360239/223235015-8684efb6-81f1-4f2c-bff9-0d877521cc90.png)


Anyone | start . inicia o processo > 1 interação com usuário (orderpizza)
Restaurante | Take order > prepare > update order >
Customer | Receive order > GATE (VERIFICAÇÃO SE O PEDIDO ESTA OK OU NÃO) > SE ESTÁ OK - PODE SER ELOGIADO - TERMINA
SE NÃO ESTÁ - RECLAMAÇÃO - TERMINA

NEM UM TIPO DE ATOR, INVADE AS ATRIBUIÇÕES DO OUTRO

5 TIPOS DE TAREFAS COM CORES DIFERENTES . CADA NÓ (TAREFA) TEM UM TÍPO ESPECÍFICO

![Screenshot 2023-03-06 at 21 32 01](https://user-images.githubusercontent.com/101360239/223235570-c2f3f0bf-74db-4146-9794-6dc009e546ce.png)
 
PRECISA DE ALGUNS ESQUEMAS PARA TER OS DADOS CORRETOS
ID - NOME DO EVENTO
TYPO - START (FORMATO)
NAME - NÃO PRECISA SER O IS MAS AJUDA A COMPLEMENTAR
PARAMENTOS > INPUT_SCHEMA
NEXT - QUAL O PRÓXIMO PASSO
LANE_ID - QUAL LANE QUE ELE PARTICIPA

![Screenshot 2023-03-06 at 21 33 23](https://user-images.githubusercontent.com/101360239/223235806-7f8937f4-3618-428c-91e1-e5bf51d059a2.png)

ID / NAME / NAME / TYPO : USERTASK (PRECISA DE UMA INTERAÇÃO COM O USUÁRIO) / LANE ID (QUALL LINHA) / PARAMETROS > ACTION (PEDIR PIZZA) INPUT > MENU > REFERENCIA DO MENU

![Screenshot 2023-03-06 at 21 34 28](https://user-images.githubusercontent.com/101360239/223236013-2e2879f6-2fab-4c0e-92f5-94a44375e036.png)

TAFERA DE SISTEMA, UMA ETAPA QUE NÃO PRECISA DO USUÁRIO PARA SER REALIZADA. 
NAME PODE SER UM POUCO MAIS VERBOSO PRA EXPLICAR MELHOR

CATEGORIA_ TAREFAS DO SISTEMA PODEM SER VÁRIAS CATEGORIAS_ UMA DAS MAIS UTILZIADAS É HTTP (QUANDO PRECISA USAR API, GET, POST)
PARAMENTERS > INPUT / REQUEST > UTL (O QUE PRECISA SER ACESSADO PARA FAZER O PEDIDO / VERB (GET) / HEADERS / CONTENTETYPE (JSON)

![Screenshot 2023-03-06 at 21 36 41](https://user-images.githubusercontent.com/101360239/223236449-98d45a65-439a-40dd-be00-e4797ebf09bd.png)

GATE COMO ELE ENVIA O PROCESSO PARA OUTRA ETAPA, TEM QUE TER MAIS DE UM NEXT >OK OR NOT OK  > QUAL O DEFAULT (PRAISE)
TYPO FLOW
LANE ID
PARAMETERS > DECISÃO > REF (RESULT)


![Screenshot 2023-03-06 at 21 38 14](https://user-images.githubusercontent.com/101360239/223236758-4937c832-5f54-48bb-940a-accb212d34a3.png)


ID
NAME
NEXT NULL (PROCESSO ENCARRO)
TYPE FINISH
LANE QUAL ETAPA TERMINOU



UMA NOVA VERSÃO DESSE PROCESSO DE PIZZA


3 PARTES DO PROJETO

DIAGRAMA (IMAGEM PNG) DO DIAGRAMA BPMN PROPOSTO

BLUEPRINT (JSON)

APRESENTAÇÃO (PUBLICAR NO SERVIDOR DO FLOWBUILD) - EMQUALQUER FORMATO MAIS A EXPLCIAÇÃO - O QUE GOSTARAM - TOMADAS DE DECISÕES - PQ TOMARAM ESSAS SOLUÇÕES

![Screenshot 2023-03-06 at 21 42 34](https://user-images.githubusercontent.com/101360239/223238993-ff2c28e9-6a25-4efd-a76d-0706fbcf7ca0.png)


SLACK
FLOWBUILD.IO
https://forms.gle/dNXU1j5L7ExYevng7
servidor para utilizar
inputes não tem um padrão / quais são os dados necessáriso para que aquela tarefa seja feita (o inpute são os patametros que devem. eu quero que o usuário escolha a pizza, o que ele precisa para fazer isso? do menu)

anotar o pedido, eu preciso fazer uma chamada para um endpoint - o sabor da pizza o que? quantidade e etc

mandar por email (segunda-feira que vem) amanha ou segunda-feira - 

cada um tem o próprio servidor (eu publiquei lá com sese nome - nomde da blueprint)
audio
gravar o video**
100% vai ter um feedback
cawemo.com para desenhar

resultado na quarta ou quinta
