## VPC Endpoints
- Permitem que você conecte sua VPC a serviços da AWS de forma privada, sem a necessidade de usar a internet, gateways, NAT ou VPNS. Eles ==proporcionam uma maneira segura e eficiente de acessar serviços AWS diretamente da sua VPC, mantendo o tráfego dentro da rede da AWS==.

- Além da velocidade, os VPC Endpoints também **podem ajudar a reduzir os custos**, uma vez que o tráfego será mantido dentro da rede AWS e nunca sairá para a internet.

- Um detalhe interessante é que os VPC Endpoints podem ter como alvo um recurso que não esteja na mesma região ou VPC, desde que o recurso seja acessível por meio de um endpoint privado.

### Tipos de VPC Endpoint:
- **Interface Endpoints**
    - ==Utiliza uma Elastic Network Interface (ENI) com endereço IP privado dentro da VPC==. Esse endpoint é conectado aos serviços AWS, com serviços que suportam a interface VPC.
    
    - Possui suporte para a maioria dos serviços da AWS.
    
	- <span style="background-color:red; color:#fff">Custo por hora e por quantidade de dados processados (CARO). </span>
	
	- **O tráfego nunca sai da rede privada da AWS**.

- **Gateway Endpoints**
    <img src="./images/gatewayEndpoint.png" alt="Gateway Endpoint Diagram"/>
    - ==É um gateway que é adicionado à sua <ins>route table</ins> para direcionar o tráfego destinado a serviços específicos==, como o S3 e Dynamo DB, tudo isso internamente pela infraestrutura da AWS.
    
	- O uso é específico para o S3 e o Dynamo DB, que suportam esse tipo de endpoint, permitindo acesso privado sem a necessidade de uma conexão pública.
    
    
	- <span style="background-color: green; color: white;font-weight:bold">Fácil de configurar e cost-free. Por isso, sempre que possível prefira usar um gateway endpoint do que uma Interface Endpoint.</span>

## Resumo
- Em suma, a única diferença entre os dois tipos é a forma de implementação.
- Se o serviço for DynamoDB ou S3, utilize um gateway endpoint sem pensar duas vezes.