# Interfaces de Rede

- Na AWS, temos diversos tipos de interfaces de rede, sendo a mais popular delas a ENI (Elastic Network Interface), vejamos alguns detalhes:

## ENI (Elastic Network Interface) - Padrão
- **Definição:** Uma ENI é uma interface de rede virtual que pode ser anexada a uma instância EC2. Ela funciona como uma interface de rede física, contendo:
  - Um endereço IP primário
  - Um ou mais endereços IP secundários,
  - Um ou mais grupos de segurança, 
  - Um endereço MAC
  - E outras configurações de rede.

- **Uso:** ENIs são usadas para conectar instâncias EC2 a sub-redes em uma VPC. Elas permitem que você mova interfaces entre instâncias, o que pode ser útil para cenários de alta disponibilidade ou para isolar diferentes tipos de tráfego.

- **Exemplo de Aplicação:** Ter múltiplas interfaces de rede em uma instância para segmentar o tráfego de rede ou para separar diferentes camadas de aplicação.
  - Um servidor com mais de uma interface de rede é chamado "Dual-Homed".



## ENA (Elastic Network Adapter) - Alta Performance
- **Definição:** O ENA é um adaptador de rede de alta performance projetado para oferecer suporte a _Enhanced Networking_ na AWS. Oferece maior largura de banda, menor latência e menor sobrecarga em comparação com as interfaces de rede padrão.

- **Uso:** ENA é usado principalmente em instâncias EC2 que exigem alta performance de rede, como em aplicações de HPC (High-Performance Computing) e grandes clusters de dados.

- **Exemplo de Aplicação:** Quando uma instância EC2 precisa de uma largura de banda de rede de até 100 Gbps, como em simulações científicas ou análises de Big Data.

## EFA (Elastic Fabric Adapter) - Potência Máxima
- **Definição:** O EFA é um adaptador de rede que fornece latência ultrabaixa e alta taxa de transferência, além de suporte para aplicativos de HPC que usam bibliotecas de comunicação de rede como MPI (Message Passing Interface). ==**O EFA possui compatibilidade limitada com Windows, tendo a performance suprimida**==

- **Uso:** EFA é especificamente projetado para workloads HPC que requerem uma comunicação de rede extremamente rápida e eficiente, como em simulações científicas, bolsa de valores ou sistemas críticos.

- **Exemplo de Aplicação:** Aplicações HPC distribuídas que exigem uma comunicação rápida entre instâncias EC2 em um cluster, como no uso industrial ou renderização gráfica em 3D.


## Limitação da quantidade de IPs na interface
- As interfaces são limitadas a uma quantidade X de endereços IP, com base no tipo da instância.

- Esse conhecimento é muito importante em workloads Kubernetes, onde os pods usarão os IPs secundários associados à ENI.

## Requester-Managed ENIs
- Para serviços gerenciados, como instâncias RDS e o control plano do EKS, a AWS efetua a criação de uma ENI gerenciada dentro da sua VPC.

- Essas interfaces são chamadas de Requester-Managed ENIs, elas não podem ser deletadas ou desacopladas das máquinas em que estão, apesar de poderem ser listadas no console.