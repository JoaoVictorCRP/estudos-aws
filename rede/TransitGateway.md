# Transit Gateway

Serviço que permite conectar múltiplas VPCs, contas da AWS e redes on-premises através de um único gateway centralizado. Ele simplifica a interconexão de redes em grande escala, permitindo que você crie uma malha de rede altamente escalável e gerenciável.

## Características

- ==A principal ideia por trás deste serviço é unir todas as redes conectadas em um único hub central, simplificando a topologia==.

- Diferentemente do VPC Peering, que não é transitivo (não permite que uma VPC conectada a outra VPC se comunique com uma terceira VPC), o Transit Gateway permite que todas as redes conectadas se comuniquem entre si, desde que as rotas estejam configuradas corretamente.

- Suporta milhares de conexões, facilitando a expansão de rede à medida que novas VPCs ou redes precisam ser integradas.

- A base fica em uma única região, porém é possível acoplar redes que estão em outras regiões.

- **Este serviço implementa o BGP (Border Gateway Protocol) para facilitar a troca de rotas entre redes on-premises e VPCs conectadas ao Transit Gateway**, otimizando o roteamento dinâmico.

  - Em exames de certificação, se cair uma questão sobre roteamento dinâmico entre redes on-premises e VPCs falando de BGP, lembre-se do Transit Gateway.

## Acoplamentos
- É possível acoplar um transit gateway com:
  - Um ou mais VPCs
  - Outro transit gateway (mesmo em outra região)
  - Conexões SD-WAN de terceiros
  - VPNs
  - Gateways Direct Connect
  - Network Function (do AWS Network Firewall)