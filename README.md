# APRESENTAÇÃO

1. [BASE](#base)
2. [SOLUÇÃO](#solucao) 
 	- 2.1. [Permitir a edição e comentário no pedido pelo Cliente](#edicao) 
	- 2.2. [Permitir o cancelamento pela Pizzaria](#cancelamento) 
 	- 2.3. [Evitar erros pela Pizzaria](#erros) 
 	- 2.4. [Evitar opinião negativa (cupom)](#cupom)  
 	- 2.5. [Evitar prejuízo (Cliente não encontrado)](#prejuizo) 
3. [DIFICULDADES E IDEIAS NÃO APLICADAS](#dificuldades)
	- 3.1. [Cliente ter atualização do status do pedido](#status) 
	- 3.2. [Cancelamento pelo Cliente](#cancelamentoc) 
	- 3.3. [Otimizador de Entrega (SubProcesso)](#otimizador)  
	- 3.4. [Retirada do Elogio/Reclamação](#elogio_reclamação)
	- 3.5. [Conectar Diagrama com JSON](#json) 
	- 3.6. [Inputs e SystemNode (HTTP)](#https) 
	- 3.7. [Envitar confusão no processo](#confusao) 
4. [CONCLUSÃO](#conclusao)

## 1. BASE <a name="base"></a>

O Desafio consiste em melhorar um processo de entrega de pedido de pizza que será implementado por uma empresa de delivery de pizza. O diagrama base foi o seguinte:

<div align="center">
<img width="100%" alt="Diagrama da Fundação" src="https://user-images.githubusercontent.com/101360239/224020626-eb0871f5-a338-4eb8-b44c-5150f8e02697.png">
</div>

Não foi fornecido o blueprint desse diagrama, porém na documentação indicada para estudo haviam alguns exemplos e schema dos nós.

## 2. SOLUÇÃO <a name="solucao"></a>

O diagrama da minha solução para o desafio é o seguinte:

![image](https://user-images.githubusercontent.com/101360239/224341687-5293c4e6-075f-4544-bd97-809350db3267.png)

Para chegar a essa solução, estudei alguns aplicativos como: iFood, PlusDelivery, telepizza e Domino's. Além do estudo dos aplicativos, dei destaque a minha experiência como usuário e discussões que já tive com amigos sobre como esses aplicativos poderiam ser aprimorados.

Os pontos mais importantes das melhorias implementadas estão em azul. Elas não representam tudo o que foi adicionado, mas são representação das ideias que tive para melhorar o projeto, podendo serem listadas na seguinte ordem: 
Permitir a edição e comentário do pedido pelo Cliente; 
Permitir o cancelamento do pedido pela Pizzaria;
Evitar erros pela Pizzaria;
Evitar opinião negativa (cupom); e 
Evitar prejuízo (cliente não encontrado).

A seguir temos uma explicação detalhada da implementação de cada um dessas ideias.

### 2.1. Permitir a edição e comentário do pedido pelo Cliente <a name="edicao"></a>

A ideia é permitir que o cliente possa editar o pedido, alterando os ingredientes, e incluindo um comentário.

<div align="center">
	
![Screenshot 2023-03-10 at 12 58 08](https://user-images.githubusercontent.com/101360239/224321948-2205162e-71d8-44bf-a680-cb5b02b2abcf.png)
	
</div>

É muito comum que os clientes tenham preferência por um ou outro ingrediente, ou até mesmo sejam alérgicos a algum deles, possibilitando a edição do pedido, o cliente pode retirar o ingrediente e efetivar uma compra. Ou seja, alguém que não iria querer comprar determinada pizza por causa de um único ingrediente, agora pode fazer a compra, já que pode excluir tal ingrediente. 

Outro ponto é poder fazer um comentário, durante a pandemia, muitas pessoas faziam compra por aplicativos de delivery e no comentário diziam que o pedido deveria ser dado ao entregador, ou transformado em gorjeta para ele. Permitir que o cliente possa comentar deixa mais fácil a personalização do pedido, sem causar maiores transtornos, por exemplo, o cliente pode informar que ele gosta muito de um ingrediente específico da pizza e pede para a pizzaria "caprichar" se puder.

Possibilitar o comentário, junto com a edição de ingredientes, torna o pedido personalizável, o que é uma forma de conseguir vender mais pizza, quanto mais personalizável, mais atraente ao cliente é.

### 2.2. Permitir o cancelamento do pedido pela Pizzaria <a name="cancelamento"></a>

Possibilitar que a Pizzaria cancele o pedido ajuda a não "quebrar" o processo. Existem situações em que não será interessante para a pizzaria atender ao pedido, como a distância para realizar a entrega, o pedido foi feito poucos minutos antes da cozinha fechar, entre outras situações. 

<div align="center">
	
![Screenshot 2023-03-10 at 12 57 47](https://user-images.githubusercontent.com/101360239/224321882-8d635804-9ee5-4b67-8ecc-a3da182deaca.png)

</div>

E mais, durante o processo de produção da pizza, pode ser que ocorra algum problema que torne impossível a finalização/entrega do pedido, portanto, também é importante que a pizzaria possa cancelar o pedido nessas situações.

Possibilitar que a pizzaria cancele o pedido, levou a criação de dois outros nós, um para realizar o reembolso do cliente e o outro para comunicar ao cliente que o pedido foi cancelado e já foi realizado o reembolso.

### 2.3. Evitar erros pela Pizzaria <a name="erros"></a>

Evitar que a pizzaria cometa erros foi a maior preocupação dessa solução, vez que uma pizza entregue errada, fora do tempo esperado, ou recebida em erro pelo cliente, pode manchar a reputação da pizzaria e gera prejuízo. 

Portanto, para evitar que o cliente tenha certeza do que está pedindo, ele deve revisar o pedido antes de realizar o pagamento.

<div align="center">
	
![Screenshot 2023-03-10 at 12 57 34](https://user-images.githubusercontent.com/101360239/224321842-44c9010f-236b-4807-bf27-43ad475f7d4e.png)

</div>

Quando a pizzaria recebe o pedido para ser aceito ou não, o cliente já aceitou fazer o pedido sabendo o tempo que ele deve demorar para ser entregue, a pizzaria também recebe o pedido para ser aceito com o prazo para entrega informado ao cliente (tempo dilatado), bem como com o tempo que ela provavelmente vai conseguir entregar (tempo real). Com isso já prevenimos que o cliente tenha uma expectativa irreal sobre o tempo de entrega e que a pizzaria erre, entregando a pizza fora do prazo. 

<div align="center">
	
![Screenshot 2023-03-10 at 12 57 21](https://user-images.githubusercontent.com/101360239/224321810-63b7c2dd-45b7-4787-ad14-aacd66cc9338.png)

</div>

Caso a pizzaria aceite o pedido, um nó de monitoramento é ativado para o sistema verificar se realmente a pizzaria consegue produzir a pizza, se tem ingredientes suficientes no estoque, se existem entregadores ativos para realizar a entrega, se aconteceu algum problema que possa evitar a confecção da pizza como falta de água, cozinha fechou, muitos pedidos já foram aceitos e etc.

Fazer o monitoramento da situação da pizzaria é muito importante, pois ajuda a evitar algum erro humano, um funcionário pode aceitar o pedido acreditando que está tudo certo, mas entre o pedido ser aceito e ele começar a ser produzido, o sistema continua verificando se está tudo certo ou não.

<div align="center">	

![Screenshot 2023-03-10 at 12 57 06](https://user-images.githubusercontent.com/101360239/224321751-f0127ed5-5207-4331-b600-21a473a66320.png)

</div>

Caso o monitoramento veja que a pizza não consegue finalizada, ele encaminha o pedido para ser cancelado e reembolsado. 

Após essa verificação, estando tudo certo, a pizza é feita. Estando pronta, passa para uma última verificação pela pizzaria antes de ser disponibilizada para entrega, se existir algum erro, volta para o nó do monitoramento.

<div align="center">
	
![Screenshot 2023-03-10 at 12 56 53](https://user-images.githubusercontent.com/101360239/224321704-2cf23c28-39fc-4ace-a9ef-4f4d52e03a09.png)

</div>

Assim a pizzaria faz verificações no momento de aceitar o pedido, enquanto espera para ser produzida e após ser produzida, evitando ao máximo ocorrer algum erro.

Por fim, ocorre uma última verificação do pedido, mas por parte do cliente, ele verifica o pedido quando é entregue a pizza, caso tenha algum erro no pedido ele é reembolsado.

<div align="center">
	
![Screenshot 2023-03-10 at 12 56 39](https://user-images.githubusercontent.com/101360239/224321642-06459333-9bf2-40e0-9351-fa1d0f9212cc.png)

</div>

Esses são os principais nós criados para evitar que ocorra algum erro que possa gerar prejuízo ou manchar a reputação da pizzaria.

### 2.4. Evitar opinião negativa (cupom) <a name="cupom"></a>

Como foi fornecido ao cliente um tempo esperado de entrega para alinhar a expectativa dele com o que será entregue, lembrando que é fornecido um tempo dilatado para que a pizzaria tenha uma margem de atraso, deve haver alguma recompensa caso o prazo para entrega seja extrapolado. 

<div align="center">
	
![Screenshot 2023-03-10 at 12 55 55](https://user-images.githubusercontent.com/101360239/224321505-741fef7b-50ca-4d7c-91f2-fcdcecf48376.png)

</div>

Assim, foi criado o nó “CUPOM DE DESCONTO”, que é fornecido ao cliente, após cliente receber a pizza. 

Para que o cliente ganhe o cupom alguns nós foram criados, primeiro o nó de tempo estipulado para entrega dilatado, que é o prazo limite, depois, o registro do horário de chegada ao local pelo entregador, com isso, é possível fazer a verificação se o prazo  foi respeitado ou não. 

<div align="center">
	
![Screenshot 2023-03-10 at 12 55 36](https://user-images.githubusercontent.com/101360239/224321420-4468e123-ed8e-44b7-843f-bbeaa8895794.png)

</div>

Se foi entregue dentro do tempo fornecido ao cliente, o processo de entrega é finalizado, se tiver ultrapassado o prazo, o cupom é gerado, enviado ao cliente e só aí que o processo é finalizado. 

E como houve a criação do cupom de desconto, também foi necessário criar o nó para o cliente poder usar o cupom antes de efetuar o pagamento.

<div align="center">
	
![Screenshot 2023-03-10 at 12 55 26](https://user-images.githubusercontent.com/101360239/224321383-9563394c-f936-42f8-a693-a8d58d07b680.png)

</div>

### 2.5 Evitar prejuízo (Cliente não encontrado) <a name="prejuizo"></a>

Essa ideia também está relacionada a evitar erro/prejuízo, entretanto, nesse ponto focamos mais em evitar que a pizzaria sofra prejuízo por culpa do cliente. 

No início do projeto eu havia pensado em possibilitar o pagamento tanto por aplicativo quanto presencialmente ao entregador, porém, com o desenvolvimento da solução, passei a questionar “E se o cliente sumir sem ter pago, o prejuízo vai ficar com a pizzaria?”. 

<div align="center">

![Screenshot 2023-03-10 at 12 55 11](https://user-images.githubusercontent.com/101360239/224321333-1b66f632-0958-4bcd-9d36-2c1b01f80b2b.png)

</div>

A partir disso, resolvi reestruturar o pagamento, para limitar o pagamento através do próprio aplicativo, ou seja, o pedido chega para ser aceito já pago, pode não ser o ideal para o cliente mas é o ideal para a pizzaria. Sendo a pizzaria nossa cliente, o foco deve ser proteger os interesses dela.

<div align="center">
	
![Screenshot 2023-03-10 at 12 54 59](https://user-images.githubusercontent.com/101360239/224321305-af0e949c-5d4d-49d5-a413-6f5805ef2337.png)

</div>

Apesar de retirar a possibilidade do cliente somente pagar quando for entregue o pedido, deixei bem sólida a tentativa de entrega, caso o cliente não seja encontrado, o entregador deve tentar entrar em contato com ele duas vezes, no espaço de 5 (cinco) minutos, caso não consiga contato, é registrada as tentativas e a pizza é devolvida a pizzaria.

<div align="center">
	
![Screenshot 2023-03-10 at 12 54 45](https://user-images.githubusercontent.com/101360239/224321268-29be4655-a26c-42b1-bede-944855a11f44.png)

</div>

E para evitar um “desencontro” o cliente fornece os dados de quem vai receber o pedido e revisa esses dados, não dando espaço para ele argumentar que “não viu que errou”.

<div align="center">
	
![Screenshot 2023-03-10 at 12 54 28](https://user-images.githubusercontent.com/101360239/224321218-72dc6bdd-7215-47b3-bf2f-5bf3e31054c1.png)
	
</div>

Essas foram ideias aplicadas para melhorar o projeto base, tornando o processo de entrega de pizza muito mais seguro tanto para a pizzaria quanto para o cliente.

## 3. DIFICULDADES E IDEIAS NÃO APLICADAS <a name="dificuldades"></a>

### 3.1. Cliente ter atualização do status do pedido <a name="status"></a>

Tentei implementar uma forma do cliente conseguir ver o status do pedido e ele ser atualizado em vários pontos (algo parecido com o que a Domino’s faz). 

O problema que tive para tentar implementar isso foi tentar não cair em um loop de atualização, o que iria travar o processo.  

<div align="center">
	
![Screenshot 2023-03-10 at 12 54 13](https://user-images.githubusercontent.com/101360239/224321158-d72fe5d1-ab03-4ae6-b7c3-c5ba4dfd5e62.png)

</div>

O mais próximo de conseguir a implementação evitando o loop foi a seguinte solução:

<div align="center">
	
![Screenshot 2023-03-10 at 12 53 57](https://user-images.githubusercontent.com/101360239/224321104-f5c0be75-25a3-4635-92de-e9068f3d8311.png)

</div>

No momento em que o pedido fosse enviado, além de comunicar a pizzaria, também abriria um novo caminho para atualização do status. Os caminhos voltariam a se conectar no momento em que cliente e entregador se encontrassem. 

No momento em que estava passando o diagrama para a primeira versão do blueprint (JSON), percebi que dava erro quando o next do systemTask continha dois caminhos. 

<div align="center">

<img width="384" alt="Screenshot 2023-03-10 at 13 48 11" src="https://user-images.githubusercontent.com/101360239/224332378-50b880ee-dfdc-4d1e-8f80-10c5bed3a87e.png">
	
</div>

Verifiquei junto aos exemplos de blueprint da documentação do flowBuild e percebi que todos tinham uma única direção, o fluxo não pode ser dividido em mais caminhos.

Antes de verificar essa impossibilidade eu tinha até mesmo pensando em colocar a verificação do status como um subprocesso, se ele fosse executável de forma assíncrona. 

Não foi possível incluir a atualização do status do pedido, mas com a estimativa de tempo de entrega e a comunicação do cancelamento do pedido/reembolso, achei que seria o suficiente de informação a ser enviada ao cliente. 

### 3.2. Cancelamento pelo Cliente <a name="cancelamentoc"></a>

Da mesma forma que o status do pedido, havia incluído a possibilidade do cliente cancelar antes da pizzaria aceitar o pedido. Porém, pelo mesmo motivo da impossibilidade de manter dois caminhos ativos, resolvi retirar esse poder e manter só com a pizzaria.

Esse também foi um dos motivos do cliente ter que revisar o pedido antes de efetuar o pagamento, ter noção do tempo de entrega, ocorrer as duas tentativas de contato quando entregador chega ao local e ele verificar se o pedido está correto no momento da entrega. 

### 3.3. Otimizador de Entrega (SubProcesso) <a name="otimizador"></a>
Também havia criado um “otimizador de entregas”, como um subprocesso, respeitando o fluxo do processo. 

<div align="center">
	
<img width="407" alt="Screenshot 2023-03-10 at 12 51 50" src="https://user-images.githubusercontent.com/101360239/224320713-80522bb4-7770-40f2-ace2-f0f656a6643f.png">
	
</div>

<div align="center">

![Screenshot 2023-03-10 at 12 53 04](https://user-images.githubusercontent.com/101360239/224320936-7748d4bb-ef2c-48da-9943-be07965bdd88.png)

</div>

Ele juntava os pedidos que seriam entregues em um bloco, extraia os endereços, organizava as entregas da mais próxima para a mais distante, verificava se havia entregador disponível, enviava a rota sugerida para o entregador e finalizava o subprocesso.

O problema aqui não foi com a otimização das rotas mas sim com a conclusão do processo se houvesse mais pizzas a serem entregues.

Pensando no que foi proposto como desafio, seria necessário incluir várias ramificações ao fim do processo, se era a última pizza, se alguma pizza ficou faltando ser entregue, isso deixaria a solução complexa/confusa demais para o que foi proposto.

Portanto, retirei essa ferramenta por não achar que era adequado para a solução como um todo.

### 3.4. Retirada do Elogio/Reclamação <a name="elogio_reclamação"></a>

Pelo mesmo motivo do otimizador de entrega, achei que manter sempre duas opções de ao fim de todos os encerramentos de processo deixaria a solução poluída.

Também fiquei mais seguro de retirar já que implementei a possibilidade de reembolso e cupom de desconto, caso ocorra atraso.

### 3.5. Conectar Diagrama com JSON <a name="json"></a>

Como eu nunca tinha tido contato com o flowBuild, tive um pouco de dificuldade em fazer as primeiras conversões dos diagramas para o blueprint. 

O meu primeiro arquivo JSON, baseado em um dos primeiros diagramas, ficou grande demais, com quase nenhuma informação nos inputs, e com pouca diversidade nos tipos de nós.

Mas após finalizar o primeiro rascunho da solução, diagrama e json prontos, consegui perceber os pontos mais fracos da minha solução como: paralelismo nos subprocessos, necessidade de novos nós, loop em alguns pontos e soluções duplicadas em outros.
 
Fazer o código foi a melhor forma de revisar meu diagrama e gerar novas soluções, apesar de ser a parte mais difícil também é a que gera mais frutos. 

### 3.6. Inputs e SystemNode (HTTP) <a name="https"></a>

Na documentação do flowBuild consta: 

É importante que o input contenha o mínimo de informações requeridas para que o canal possa executar a tarefa junto ao usuário. Evite enviar informações não essenciais para execução da tarefa.

Portanto, selecionar o mínimo de informação a ser fornecido é algo que precisa de muita reflexão sobre o que é essencial ou não. E mais, enviar informação desnecessária causa outros problemas como facilitar vazamento de informação, além de tornar o processo mais demorado e custoso.

Além disso, também organizei os objetos dentro da bag, para ter um catálogo do que poderia usar e onde poderia armazenar a informação.

<div align="center">	

<img width="538" alt="Screenshot 2023-03-10 at 12 51 28" src="https://user-images.githubusercontent.com/101360239/224320644-133e681d-3b54-4012-9542-390c32172e86.png">

</div>

Outro ponto que tive dificuldade foi a utilização do systemNode (HTTP), por vezes eu não tive certeza se seria melhor usar o setToBag ou HTTP. Como não ficou tão claro quando deveria utilizar um ou outro, dei preferencia para sempre usar o setToBag e somente quando tinha certeza que seria um HTTP que fazia uso dele.

<div align="center">
	
<img width="431" alt="Screenshot 2023-03-10 at 12 51 07" src="https://user-images.githubusercontent.com/101360239/224320573-e20f0925-6941-4d39-a62f-3b84481be9ff.png">

</div>

### 3.7 Evitar confusão no processo <a name="confusao"></a>

Outro desafio é evitar confusão no processo, deixar o Diagrama limpo e claro é uma tarefa que só se resolve com a confecção do rascunho e/ou apagar todo o processo e reiniciar já tendo mais bem definido o objetivo e os meios para chegar até ele. 

Comparando a minha solução definitiva com os meus processos iniciais, fica evidente como ficou mais limpo, mesmo tendo mais ferramentas. 

<div align="center">
	
![renanb (1)](https://user-images.githubusercontent.com/101360239/224320515-2b0d38a1-f134-4eb0-93bb-249f7632438a.svg)

</div>

Depois que você consegue compreender melhor o funcionamento do flowBuild fica mais fácil de organizar os nós e pensar em complementos para a solução do problema.

## 4. CONCLUSÃO <a name="conclusao"></a>

A minha solução teve como foco principal a pizzaria, proteger a pizzaria de ter prejuízo e manter sua reputação. 

Também incluí ferramentas que julguei necessárias ou muito importantes para o sucesso do processo, sem deixar complexo demais ou sem sentido. 

Projetar um resultado para o desafio levando em consideração o tempo fornecido e a experiência que tinha com ferramentas similares, também foi muito importante, bem como organizar a ordem de importância entre Diagrama / BluePrint / Apresentação.

O flowBuild se mostrou uma excelente ferramenta para organizar todo processo e, como dito pelo Gustavo na apresentação do Desafio, apesar de ter apenas 8 elementos gráficos, é possível dar uma complexidade gigantesca ao processo. 

Acredito que o maior desafio do flowBuild é esse, deixar tarefas muito complexas mais simples, bem como evitar que processos simples se tornem complexos. 

<div align="center">
	
<img width="142" alt="Screenshot 2023-03-10 at 12 50 28" src="https://user-images.githubusercontent.com/101360239/224320444-7bc923f6-0a98-4430-9252-c9669daaea50.png">

</div>


