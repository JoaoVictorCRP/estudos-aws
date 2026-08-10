# AWS Cloud WAN

- O AWS Cloud WAN é um serviço gerenciado de rede glocal que permite criar, gerenciar e monitorar WANs (Wide Area Networks) em escala, sejam elas híbridas ou totalmente na nuvem.

- Por meio deste serviço você pode configurar políticas de rede, definir topologias, automatizar o gerenciamento da rede e monitorar o tráfego de forma centralizada (através do AWS Network Manager).

- O principal problema resolvido pelo Cloud WAN é a complexidade de gerenciar redes globais, especialmente quando se trata de conectar múltiplas filiais, data centers e recursos na nuvem. Com o Cloud WAN, você pode simplificar a conectividade entre diferentes regiões da AWS e locais on-premises, garantindo alta disponibilidade, segurança e desempenho.

- Apesar de ser um serviço global, o painel central do Cloud WAN fica obrigatoriamente na região do Oregon (us-west-2), sendo a região de hospedagem do serviço.

## Componentes do Cloud WAN

- **Global Network**: É a entidade principal que representa a rede global do cliente. Dentro de uma Global Network, você pode criar e gerenciar diferentes topologias de rede, como hub-and-spoke ou full mesh.

- **Core Network**: É a rede central que conecta diferentes regiões da AWS e locais on-premises. Você pode criar múltiplas Core Networks dentro de uma Global Network, cada uma com suas próprias políticas de roteamento e topologias.
  - **Core Network Edge (CNE)**: Ponto de conexão regional de uma Core Network, atuando de maneira semelhante ao [Transit Gateway](./TransitGateway.md), permitindo a ligação com recursos locais via Attachments.

  - **Core Network Polic (CNP)**: Conjunto de regras que definem como o tráfego deve ser roteado dentro da Core Network. As políticas podem incluir regras de filtragem, priorização e encaminhamento de tráfego.

- **Network Segments**: Após conectar as redes por meio dos CNEs, você pode criar Network Segments, que funcionam de maneira semelhante aos routing domains do Transit Gateway, permitindo a segmentação do tráfego e a aplicação de políticas específicas para diferentes tipos de tráfego.

- **Attachments**: São as conexões entre os CNEs e os recursos da AWS, como VPCs, VPNs e Direct Connect. Cada attachment é associado a um Network Segment, permitindo que o tráfego seja roteado de acordo com as políticas definidas.
  - **Os Attachments podem ser: VPCs, Site-to-Site VPNs, Transit Gateways, Direct Connect e Connects (SDWANs via túnel GRE)**.