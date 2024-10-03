## VPC Endpoints
Permitem que você conecte sua VPC a serviços da AWS de forma privada, sem a necessidade de usar a internet, gateways, NAT ou VPNS. Eles <span style="background-color: #e0a800; color: black;font-weight:bold">proporcionam uma maneira segura e eficiente de acessar serviços AWS diretamente da sua VPC, mantendo o tráfego dentro da rede da AWS.</span>

Além da velocidade, os VPC Endpoints também podem ajudar a reduzir os custos, uma vez que o tráfego será mantido dentro da rede AWS e nunca sairá para a internet.

### Tipos de VPC Endpoint:
- **Interface Endpoints**
    - <span style="background-color: #e0a800; color: black;font-weight:bold">Utiliza uma Elastic Network Interface (ENI) com endereço IP privado dentro da VPC.</span> Esse endpoint é conectado aos serviços AWS, com serviços que suportam a interface VPC.
    
    - Possui suporte para a maioria dos serviços da AWS.
    
	- Custo por hora e por quantidade de dados processados (**CARO**).
	
	- **O tráfego nunca sai da rede privada da AWS**.

- **Gateway Endpoints**
    ![alt text](gatewayEndpoint.png)
    - <span style="background-color: #e0a800; color: black;font-weight:bold">É um gateway que é adicionado à sua tabela de rotas para direcionar o tráfego destinado a serviços específicos</span>, como o S3 e Dynamo DB, tudo isso internamente pela infraestrutura da AWS.
    
	- O uso é específico para serviços como S3 e o Dynamo DB, que suportam esse tipo de endpoint, permitindo acesso privado sem a necessidade de uma conexão pública.
    
	- Possui suporte para S3 e DynamoDB.
    
	- <span style="background-color: green; color: white;font-weight:bold">Fácil de configurar e cost-free, sempre que possível prefira usar um gateway endpoint do que uma Interface Endpoint.</span>

Em suma, a única diferença entre os dois tipos é a forma de implementação