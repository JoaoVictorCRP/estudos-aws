# Largura de Banda

- Cada serviço de rede possui um limite de largura de banda.
  - A largura de banda é a quantidade máxima de dados que podem ser transmitidos em um determinado período de tempo, geralmente medida em bits por segundo (bps).

- O tamanho da largura de banda é um fator crucial na hora de escolher qual serviço, arquitetura ou tecnologia utilizar, pois impacta diretamente na performance da rede e na experiência do usuário.

- Vejamos abaixo os limites de largura de banda para cada serviço de rede da AWS:

## Site-to-Site VPN
- Até 1,25 Gbps por túnel (lembrando que cada conexão traz 2 túneis, mas o roteamento ativo/passivo faz com que apenas 1 túnel seja utilizado por vez, então a largura de banda efetiva é de 1,25 Gbps).

- Ao conectar com um Transit Gateway ou Cloud WAN, também é possível ativar o modo Large Bandwidth Tunnel (LBT), que garante até 5 Gbps por túnel.


## Direct Connect
- Há duas modalidades de conexão física e lógica, que impactam na largura de banda:
  - **Dedicated Connection**: 1Gbps, 10Gbps, 100Gbps e 400Gbps (dependendo do tipo de conexão escolhida).
  - **Hosted Connection**: de 50Mbps até 25Gbps (dependendo do provedor de serviços e do tipo de conexão escolhida).
    - *Detalhe importante: Em hosted connections, a AWS aplica uma política de tráfego rígida, que faz com que rajadas que ultrapassam a largura de banda contratada sejam descartadas*.

## Transit Gateway
- A largura de banda varia conforme o tipo de acoplamento:
  - **VPC Attachment**: até 100 Gbps por AZ.
  
  - **Direct Connect Attachment**: até 100 Gbps.
  
  - **TGW Peering Attachment (Inter/Intra-Region)**: Até 100 Gbps.
  
  - **TGW Connect Attachment**: até 5 Gbps por túnel, sendo que você pode criar até 4 túneis por conexão, totalizando 20 Gbps por conexão.

  - **VPN Attachment**: Segue as regras do Site-to-Site VPN, ou seja, até 1,25 Gbps por túnel.

## VPC Peering
- Largura de banda **não possui limite teórico**, mas na prática é limitada pela capacidade das ENI envolvidas na comunicação entre as VPCs.