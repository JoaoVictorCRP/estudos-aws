# Direct Connect

- O Direct Connect (DX) é um serviço que permite estabelecer uma conexão de rede privada cabeada entre a infraestrutura local e a AWS.

- Segue o mesmo conceito de conexão híbrida do Site to Site VPN, porém o paradigma é outro. Enquanto o S2S VPN utiliza a internet para estabelecer a conexão, o Direct Connect utiliza uma conexão dedicada, o que garante maior estabilidade e menor latência.

- O grande diferencial do Direct Connect é, acima de tudo, a baixa latência e a largura de banda alta, essencial para aplicações de alta performance, ou ambientes que necessitam de transferência de grandes volumes de dados entre o on-premises e a AWS.

- O valor da transferência de dados do Direct Connect é mais barato do que o valor da transferência de dados da internet pública, o que pode gerar uma economia significativa para empresas que necessitam transferir grandes volumes de dados entre a AWS e a infraestrutura local.
  - Apesar disso, o custo inicial pra fazer a conexão do Direct Connect é alto, pois envolve a contratação de um provedor parceiro e a instalação de uma conexão física dedicada.

- **O tempo de provisionamento de uma conexão do Direct Connect varia de 4 a 12 semanas**, dependendo da disponibilidade do provedor parceiro e da complexidade da configuração. 
  - Leve isso em consideração ao planejar a implementação do Direct Connect, pois o tempo de provisionamento pode impactar o cronograma do projeto.


## Tipos de Conexão
- Há duas formas de se conectar ao Direct Connect: através de uma conexão dedicada (Dedicated Connection) ou através de uma conexão hospedada (Hosted Connection).

- **Dedicated Connection (Conexão Dedicada)**:

  - Porta física na AWS dedicada exclusivamente à sua conta.
  - Capacidades: 1 Gbps, 10 Gbps, 100 Gbps e 400 Gbps.
  - VIFs: Permite criar múltiplas Virtual Interfaces (Public, Private, Transit VIFs) na mesma conexão.

- **Hosted Connection (Conexão Hospedada)**:

  - Provisionada por um parceiro credenciado (AWS Direct Connect Partner) sobre uma porta física mantida pelo parceiro.
  - Capacidades: De 50 Mbps até 25 Gbps (com capacidade de banda alocada e garantida pela AWS/Parceiro, sem degradação por compartilhamento).
  - Limitação: Suporta apenas 1 Virtual Interface (VIF) por conexão hospedada.

## VIFs (Virtual Interfaces)
- As VIFs são interfaces virtuais que permitem a comunicação entre a rede on-premises e a AWS através do Direct Connect. Elas são criadas sobre a conexão física (Dedicated ou Hosted) e podem ser de três tipos: Public, Private e Transit.

- **Public VIF**: Permite o acesso a serviços públicos da AWS, como S3, DynamoDB e outros serviços públicos, utilizando endereços IP públicos.
  - Apesar de o acesso ser por um endereço IP público, o tráfego não passa pela internet pública, mas sim pela conexão privada do Direct Connect, garantindo maior segurança e desempenho.

- **Private VIF**: Permite o acesso a recursos privados dentro de uma VPC, utilizando endereços IP privados.

- **Transit VIF**: Permite o acesso a múltiplas VPCs através do AWS Transit Gateway, utilizando endereços IP privados.

## As camadas do DX no modelo OSI

- O DX é um serviço multi-camadas, tendo 3 componentes diferentes, cada um operando em uma camada diferente do modelo OSI.

- **Camada 1 (Física)**: Conexão via fibra óptica conectando o roteador do cliente/parceiro ao roteador da AWS na Direct Connect Location.

- **Camada 2 (Enlace)**: Uso de VLANs (encapsulamento IEEE 802.1Q) para segmentar o tráfego. Cada VLAN é associada a uma Virtual Interface (VIF) específica.

- **Camada 3 (Rede)**: Uso obrigatório do BGP (Border Gateway Protocol) para anúncio e troca de rotas dinâmicas entre o roteador on-premises e a AWS.