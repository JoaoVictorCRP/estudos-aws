## VPC Endpoints
- Permitem que você conecte sua VPC a serviços da AWS de forma privada, sem a necessidade de usar a internet, gateways, NAT ou VPNS. Eles <span style="background-color: #e0a800; color: black;font-weight:bold">proporcionam uma maneira segura e eficiente de acessar serviços AWS diretamente da sua VPC, mantendo o tráfego dentro da rede da AWS.</span>

- Além da velocidade, os VPC Endpoints também **podem ajudar a reduzir os custos**, uma vez que o tráfego será mantido dentro da rede AWS e nunca sairá para a internet.

### Tipos de VPC Endpoint:
- **Interface Endpoints**
    - <span style="background-color: #e0a800; color: black;font-weight:bold">Utiliza uma Elastic Network Interface (ENI) com endereço IP privado dentro da VPC.</span> Esse endpoint é conectado aos serviços AWS, com serviços que suportam a interface VPC.
    
    - Possui suporte para a maioria dos serviços da AWS.
    
	- <span style="background-color:red; color:#fff">Custo por hora e por quantidade de dados processados (CARO). </span>
	
	- **O tráfego nunca sai da rede privada da AWS**.

- **Gateway Endpoints**
    ![alt text](gatewayEndpoint.png)
    - <span style="background-color: #e0a800; color: black;font-weight:bold">É um gateway que é adicionado à sua <ins>route table</ins> para direcionar o tráfego destinado a serviços específicos</span>, como o S3 e Dynamo DB, tudo isso internamente pela infraestrutura da AWS.
    
	- O uso é específico para o S3 e o Dynamo DB, que suportam esse tipo de endpoint, permitindo acesso privado sem a necessidade de uma conexão pública.
    
    
	- <span style="background-color: green; color: white;font-weight:bold">Fácil de configurar e cost-free. Por isso, sempre que possível prefira usar um gateway endpoint do que uma Interface Endpoint.</span>

## Resumo
- Em suma, a única diferença entre os dois tipos é a forma de implementação.
- Se o serviço for DynamoDB ou S3, utilize um gateway endpoint sem pensar duas vezes.