O AWS Wavelength é um serviço projetado para criar aplicações mobile com latências excepcionalmente baixas. Ele faz isso ao integrar recursos de computação e armazenamento da AWS diretamente nas redes 5G de **provedores de serviços de telecomunicação (CSPs)**, ou seja, na ==borda da rede 5G==.

## Componentes

- **Wavelenth zones**: É uma implantação de infraestrutura que fica incorporada dentro dos data centers dos provedores de serviços de telecomunicações, essas zones são responsáveis por integrar recursos da AWS com as redes 5G.

- **Carrier gateways**: Funcionam como um ponto de conexão que permite que o tráfego de aplicações de dispositivos 5G acesse diretamente os recursos da AWS implantados nas **Zonas Wavelength**. Essencialmente, os carrier gateways são o elo entre a sua Virtual Private Cloud (VPC) estendida para a Zona Wavelength e a rede 5G do provedor de telecomunicações.

## Como funciona?
- O Wavelength estende uma VPC da AWS para uma ou mais zonas Wavelength, que são implantações de infraestrutura dentro dos data center dos provedores de telecomunicação.

- A proximidade com os dispositivos 5G permite que o tráfego de aplicativos chegue aos servidores nessas zonas ==**sem precisar atravessar a internet pública**==, minimizando a latência e aproveitando a alta largura de banda das redes 5G modernas. ==O tráfego não sai da rede do provedor de serviços de comunicação.==

- **Serviços AWS Suportados**: Dentro das Zonas Wavelength, você pode criar **instâncias EC2, volumes EBS, sub-redes VPC e _carrier gateways_**. Serviços como Systems Manager, CloudWatch, CloudTrail, CloudFormation e Application Load Balancer (ALB) também podem ser utilizados.

