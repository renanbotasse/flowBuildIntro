# APRESENTAÇÃO

1. [BASE](#base)
2. [SOLUÇÃO](#solucao) 
 	- 2.1. [Permitir edição e comentário no pedido pelo Cliente](#edicao) 
	- 2.2. [Permitir cancelamento pela Pizzaria](#cancelamento) 
 	- 2.3. [Evitar erros pela Pizzaria](#erros) 
 	- 2.4. [Evitar impressão negativa - Cupom de desconto](#cupom)  
 	- 2.5. [Evitar prejuízo (Cliente não encontrado)](#prejuizo) 
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

O Desafio consiste em fazer um processo de entrega de pedido de pizza a ser implementado por uma empresa de delivery de pizza. Foi fornecido pela fundação o diagrama abaixo para ser melhorado.

<img width="100%" alt="Diagrama da Fundação" src="https://user-images.githubusercontent.com/101360239/224020626-eb0871f5-a338-4eb8-b44c-5150f8e02697.png">

Não foi fornecido a blueprint desse diagrama, porém na documentação indicada para estudo haviam alguns exemplos, além dos próprios schema dos nós.

## 2. SOLUÇÃO <a name="solucao"></a>

O Diagrama da minha solução do Desafio é o seguinte:

![renanb (6)](https://user-images.githubusercontent.com/101360239/224022944-102ba1fa-7e37-4156-afad-09aac2a2d527.png)

Para chegar a essa solução, estudei alguns aplicativos como: [iFood](https://www.ifood.com.br/?toHome=true), [PlusDelivery](https://www.plusdelivery.com.br/), [telepizza](https://www.telepizza.pt/) e [Domino's](https://www.dominospizza.pt/). E também dei ênfase na minha experiência como usuário e discussões que já tive com amigos sobre o que os aplicativos deveriam aprimorar. 

Os principais pontos que quis implementar no projeto base estão em azul, podendo serem listados na seguinte ordem: Permitir edição e comentário pelo Cliente, Permitir cancelamento pela Pizzaria, Evitar erros pela Pizzaria, Evitar impressão negativa - Cupom de desconto e Evitar prejuízo (Cliente não encontrado). 

A seguir temos uma explicação detalhada da implementação de cada um desses aspectos.

### 2.1. Permitir edição e comentário no pedido pelo Cliente <a name="edicao"></a>

Permitir que o cliente edite o pedido, alterando os ingredientes e fazendo comentários. 

É muito comum pessoas gostarem de determinado pizza mas não gostarem de um item em específico, ou terem alergia a ele, um exemplo seria uma pizza dentre seus inúmeros ingredientes, contenha pimentão e o usuário não gosta. Ele pode pedir para retirar o ingrediente e conseguimos garantir uma compra a mais. 

Outro ponto é o comentário, durante a pandemia, muitas pessoas faziam uma compra por aplicativos de delivery e nos comentários diziam que o pedido deveria ser dado ao entregador, ou transformado em gorjeta para ele. Permitir que o cliente faça um comentário deixa mais fácil a personalização do pedido, sem causar maiores transtornos, por exemplo, o cliente pode informar que ele gosta muito de um ingrediente específico da pizza e pede para a pizzaria "caprichar" se puder. 

Possibilitar o comentário, junto com a edição de ingredientes, torna o pedido personalizavel, o que torna mais próximo com a realidade, já que é comum esse tipo de ferramenta.

<div align="center">
	
<img width="450" height="300" align="center" alt="edição e comentário no pedido" src="https://user-images.githubusercontent.com/101360239/224022618-a40cd5b2-3d7b-4239-bbbc-75291766a725.png">

</div>

	
### 2.2. Permitir cancelamento pela Pizzaria <a name="cancelamento"></a>

Possibilitar que a Pizzaria cancele o pedido ajuda a não "quebrar" o processo. Se o cliente mora muito longe e faz o pedido? Se o cliente faz o pedido mas a cozinha da pizzaria já fechou? Existem várias situações que a pizzaria pode não querer atender determinado pedido. 

Ou se a pizzaria tiver algum problema durante a confecção da pizza, tornando impossível sua conclusão, deve ser possível cancelar o pedido.

O cancelamento do pedido pela pizzaria leva a duas situações, fazer o reembolso do que foi pago pelo usuário e avisar ao usuário desse reembolso/cancelamento.

<div align="center">

<img width="626" alt="cancelamento pela Pizzaria" src="https://user-images.githubusercontent.com/101360239/224136316-58e5132b-6e05-46db-8513-a583da790ad9.png">

</div>	
	
### 2.3. Evitar erros pela Pizzaria <a name="erros"></a>

+ Cliente revisa
+ Recebe pedido com tempo real e dilatado
+ Pode não aceitar
+ Monitoramento da pizzaria (acidente, luz, ingredientes)
+ Cancelar
+ Revisar pedido na pizzaria
+ Cliente revisa na entrega
+ Atraso gera desconto futuro

<div align="center">
<img width="264" alt="cliente revisa pedido" src="https://user-images.githubusercontent.com/101360239/224141427-4bbdfa3b-5bc6-4285-b31c-f420de443d2d.png">

<img width="870" alt="pizzaria revisa pedido e pizza" src="https://user-images.githubusercontent.com/101360239/224023218-7573f4c0-c043-4fdf-a78c-2207779de122.png">
	
<img width="195" alt="cliente revisa pizza" src="https://user-images.githubusercontent.com/101360239/224142384-0e08e4f9-e090-4dd4-9f6c-2c0d817e2403.png">

<img width="563" alt="cupom pelo atraso" src="https://user-images.githubusercontent.com/101360239/224142017-53b656cb-e849-48c9-9c00-a0a02192e351.png">

</div>
	
### 2.4. Evitar impressão negativa - Cupom de desconto <a name="cupom"></a>

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
	
### 2.5 Evitar prejuízo (Cliente não encontrado) <a name="prejuizo"></a>

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
	
## 3. DIFICULDADES E IDEIAS NÃO APLICADAS  <a name="dificuldades"></a>

### 3.1. Cliente ter atualização do status do pedido<a name="status"></a>

<div align="center">

<img width="613" alt="Screenshot 2023-03-09 at 12 34 30" src="https://user-images.githubusercontent.com/101360239/224024629-ebbe0973-5881-4560-98f5-b144ab4c45d4.png">

</div>
	
Loop

Paralelismo/Serialismo

### 3.2. Cancelamento pelo Cliente <a name="cancelamentoc"></a>

Paralelismo/Serialismo

### 3.3. Otimizador de Entrega (SubProcesso)<a name="otimizador"></a>

Mais que um pedido, inúmeros nós ao final. Ficaria complexo demais para o que foi proposto.

<div align="center">

<img width="623" alt="Screenshot 2023-03-09 at 12 47 36" src="https://user-images.githubusercontent.com/101360239/224027491-d7244102-903e-456e-a934-dba4686350fb.png">

</div>

<div align="center">

<img width="1087" alt="Screenshot 2023-03-09 at 14 23 24" src="https://user-images.githubusercontent.com/101360239/224054051-aeff82a6-da8a-4780-bc22-aa22c2502f38.png">

</div>
	
### 3.4. Retirada do Elogio/Reclamação <a name="elogio_reclamação"></a>

Substitui pelo Cupom - Acho mais efetivo

### 3.5. Conectar Diagrama com JSON <a name="json"></a>

### 3.6. Inputs e SystemNode (HTTPS)<a name="https"></a>

<div align="center">

<img width="621" alt="Screenshot 2023-03-09 at 14 27 28" src="https://user-images.githubusercontent.com/101360239/224055074-94824a85-e237-4b26-ac6f-c277559436c9.png">

</div>

<div align="center">

<img width="430" alt="Screenshot 2023-03-09 at 14 25 19" src="https://user-images.githubusercontent.com/101360239/224054622-e865b3b6-3f48-4950-bcf0-432b791d2b70.png">

</div>
		
### 3.7 Envitar confusão no processo<a name="confusao"></a>

<div align="center">

<img width="50%" alt="Screenshot 2023-03-09 at 12 45 10" src="https://user-images.githubusercontent.com/101360239/224026856-6856f2c7-04f0-487c-9831-c868209a1155.png">

</div>
	
## 4. CONCLUSÃO <a name="conclusao"></a>

Diagramas e Nós são boas formas de organizar
Lanes e permissões dão segurança
Gateways dão opções e evita problemas já que é serialismo.
