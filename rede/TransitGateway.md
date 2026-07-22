# Transit Gateway

Serviço que permite conectar múltiplas VPCs, contas da AWS e redes on-premises através de um único gateway centralizado. Ele simplifica a interconexão de redes em grande escala, permitindo que você crie uma malha de rede altamente escalável e gerenciável.

## Características

- ==A principal ideia por trás deste serviço é unir todas as redes conectadas em um único hub central, simplificando a topologia==.

- Diferentemente do VPC Peering, que não é transitivo (não permite que uma VPC conectada a outra VPC se comunique com uma terceira VPC), o Transit Gateway permite que todas as redes conectadas se comuniquem entre si, desde que as rotas estejam configuradas corretamente.
  - A comunicação de cada nó de rede com todos os outros é chamado de **Full Mesh**, enquanto que a comunicação de cada nó de rede com apenas um outro nó é chamado de **Point-to-Point**.

- Suporta milhares de conexões, facilitando a expansão de rede à medida que novas VPCs ou redes precisam ser integradas.

- A base fica em uma única região, porém é possível acoplar redes que estão em outras regiões.

- **Este serviço implementa o BGP (Border Gateway Protocol) para facilitar a troca de rotas entre redes on-premises e VPCs conectadas ao Transit Gateway**, otimizando o roteamento dinâmico.

  - Em exames de certificação, se cair uma questão sobre roteamento dinâmico entre redes on-premises e VPCs falando de BGP, lembre-se do Transit Gateway.

## Acoplamentos
- É possível acoplar um transit gateway com:
  - Um ou mais VPCs
  - Outro transit gateway (mesmo em outra região)
  - Conexões SD-WAN de terceiros (conhecido como TGW Connect)
    - Esta conexão é feita por meio de um túnel GRE (Generic Routing Encapsulation) entre o Transit Gateway e o dispositivo SD-WAN.
    - A largura de banda da conexão TGW Connect é limitada a 5 Gbps por túnel,e você pode criar até 4 túneis por conexão, totalizando 20 Gbps por conexão.
  - VPNs
  - Gateways Direct Connect
  - Network Function (do AWS Network Firewall)

## As rotas no TGW
- O TGW centraliza as rotas de todas as redes conectadas a ele, porém cada VPC também tem sua route table, que aponta para o TGW.

- Uma vez que a VPC é acoplada ao TGW e a tabela de rotas da subrede acoplada ajustado para apontar para o TGW a partir de uma rota genéria, como 10.0.0.0/8 ou 0.0.0.0/0, as rotas de saída para outras VPCs são totalmente gerenciados pelo TGW.

## Routing Domains
- No Transit Gateway, routing domains são agrupamentos lógicos de tabelas de rotas, que podem ser usados para isolar o tráfego entre diferentes grupos de VPCs e redes on-premises conectadas ao TGW.

- Essa funcionalidade permite que diferentes grupos de VPCs e redes on-premises se comuniquem entre si de forma isolada.

- Você pode, por exemplo, fazer com que uma VPN se conecte com todas as VPCs acopladas ao TGW e, ao mesmo tempo, impedir que uma VPC se comunique com outra VPC acoplada ao mesmo TGW.
  - Isto é feito através da criação de um routing domain para a VPN e outro para as VPCs, garantindo que o tráfego seja isolado entre eles.
  
  - Diagrama visual da arquitetura:

  ![Diagrama de Routing Domains](./images/routingDomains.png)

## Considerações sobre AZs
- Apesar do acoplamento do TGW ser feito a nível de VPC, o roteamento opera a nível de AZ, o que significa que **cada AZ precisa ter uma sub-rede acoplada ao TGW para que o tráfego possa ser roteado corretamente entre as VPCs e redes on-premises conectadas**.

## Appliance Mode

- O Appliance Mode é uma funcionalidade ativada no VPC Attachment do Transit Gateway, projetada para arquiteturas de inspeção centralizada com appliances stateful (firewalls, IDS/IPS).

- Por padrão, o TGW prioriza manter o tráfego na mesma AZ de origem (**AZ Affinity**). Na volta do tráfego (resposta), ele pode usar ECMP e entregar o pacote por uma AZ/ENI diferente da que recebeu a ida.

  - Esse fluxo de ida por uma AZ (Firewall A) e volta por outra AZ (Firewall B) faz com que o Firewall B receba tráfego de uma sessão que ele não conhece, descartando os pacotes (Stateful Drop), causando problemas de conectividade.

- Quando o Appliance Mode é ativado no attachment da VPC de Inspeção, ele força o TGW a usar a mesma AZ/ENI do anexo tanto para o tráfego de ida quanto para o de volta durante toda a vida daquela sessão TCP/UDP, garantindo a simetria no firewall, e o conhecimento total do estado da sessão, evitando o problema de Stateful Drop.

- Deixar o appliance mode desativado é ideal para tráfego entre VPCs comuns sem firewalls no meio, mantendo a menor latência e evitando custos de dados cross-AZ desnecessários.

## Multicast no TGW
- O Transit Gateway possui suporta para Multicast, permitindo que uma máquina envie pacotes para múltiplos destinos simultaneamente, sem a necessidade de enviar cópias separadas para cada destino.

- **A habilitação do Multicast deve ser feita no momento da criação do TGW, e não pode ser habilitado posteriormente**.

- O multicast do TGW suporta tanto o mapeamento estático quanto o dinâmico (via IGMP), permitindo que os destinos se inscrevam e recebam pacotes de forma eficiente.

- A configuração dos destinos é feita por meio da criação de grupos multicast, que incluem os hosts que desejam receber os pacotes multicast. Cada grupo multicast é identificado por um endereço IP multicast específico.

- O roteamento multicast não suporta AWS Direct Connect, Site-to-Site VPN ou outro Transit Gateway, apenas VPCs acopladas ao mesmo TGW podem participar do multicast.

  - **Se você quiser fazer multicast entre a VPC e uma rede on-premises, você precisará de um appliance de rede que suporte o estabelecimento de túneis GRE (Generic Routing Encapsulation) entre a VPC e a rede on-premises**, via Direct Connect ou Site-to-Site VPN, e que seja capaz de encapsular e decapsular os pacotes multicast.

- Instâncias EC2 de antiga geração (não-Nitro) não suportam multicast a menos que você desabilite o Source/Destination Check na interface de rede da instância. Instâncias Nitro suportam multicast sem a necessidade de desabilitar o Source/Destination Check.