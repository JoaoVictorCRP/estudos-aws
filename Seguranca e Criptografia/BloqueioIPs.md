Para realizar o bloqueio de um IP indesejado podemos montar diversas arquiteturas. Vamos checar as nossas linhas de defesa:


## Bloqueando no NACL 
- ==Esse é o tipo de bloqueio mais comum, fácil e barato.==

- Basta criar uma regra de negação para o IP do cliente na NACL, isso faz com que ele fique bloqueado de cara.

- É um erro pensar que é possível bloquear um cliente pelo security group, os security groups só podem ter regras de permissão, não tem regras de negação.

![[nacl-block.png]]


### Bloqueando a nível de Software
- É possível também bloquear o cliente pelo IP com algum software instalado na sua instância, como por exemplo, o iptables e UFW.

- Ainda que seja algo trivial, é um ato meio idiota, pois **de qualquer forma, o pedido do cliente vai atravessar a sua rede, chegar na sua máquina e fazer o processador tomar a decisão de dar um Deny.** Poxa, isso isso faz com que você consuma recursos, e em larga escala, pode até sair caro.
![[software-block.png]]

### Bloqueando com ALB
- Quando temos um Application Load Balancer como ponto intermediário entre o cliente e a instância, ocorrerá um processo chamado "Connection Termination"
	
	- Connection Termination ocorre para encerrar a conexão com o cliente, a partir daí quem faz a conexão com a instância é o próprio ALB. O ALB age basicamente como o mensageiro.
	
	- E sim, o IP que vai chegar na instância não é mais o do cliente, e sim do ALB.

- Nesse caso, nossa única linha de defesa será o NACL, portanto, volte na explicação... [[BloqueioIPs#Bloqueando no NACL]]
![[alb-block.png]]


### Bloqueando com o WAF
- É possível colocar o Web Application Firewall para filtrar os IPs que batem no ALB.

- ==Esse é uma técnica bem eficiente, porém mais cara==.
![[waf-block.png]]

### Bloqueando peloCloudFront
- Tá certo, em uma arquitetura que utiliza CloudFront, precisamos ter duas coisas em mente: 
	- O CloudFront não faz parte da VPC. 
	- ==Todas as requisições que chegam aos recursos dentro da VPC tem como origem o IP público do CloudFront== (basicamente, Connection Termination)

- Sendo assim, devemos varrer o IP indesejado antes do CloudFront passar pra frente.

- Para isso, basta colocar um WAF nesse CloudFront aí, mas cuidado... Isso sai mais caro.

- Se você quiser bloquear um país inteiro, da pra fazer isso direto no CloudFront, com o recurso de georestriction.

![[cloudfront-block.png]]
