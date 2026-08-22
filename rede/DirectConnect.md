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
  - **Limitação: Suporta apenas 1 Virtual Interface (VIF) por conexão hospedada**.

## VIFs (Virtual Interfaces)
- As VIFs são interfaces virtuais que permitem a comunicação entre a rede on-premises e a AWS através do Direct Connect. Elas são criadas sobre a conexão física (Dedicated ou Hosted) e podem ser de três tipos: Public, Private e Transit.

- **Public VIF**: Permite o acesso a serviços públicos da AWS, como S3, DynamoDB e outros serviços públicos, utilizando endereços IP públicos (pertencentes à AWS).
  - Apesar de o acesso ser por um endereço IP público, o tráfego não passa pela internet pública, mas sim pela conexão privada do Direct Connect, garantindo maior segurança e desempenho.

- **Private VIF**: Permite o acesso a recursos privados dentro de uma VPC, utilizando endereços IP privados.

- **Transit VIF**: Permite o acesso a múltiplas VPCs através do AWS Transit Gateway, utilizando endereços IP privados.

- Há também um outro tipo de VIF, chamado **Hosted VIF** (NÃO CONFUNDIR COM HOSTED CONNECTION), que é uma VIF criada em uma conta AWS diferente da conta que possui a conexão física do Direct Connect. Ela pode assumir qualquer um dos três tipos de VIFs (Public, Private ou Transit), com o diferencial de ser em uma conta separada.

## As camadas do DX no modelo OSI

- O DX é um serviço multi-camadas, tendo 3 componentes diferentes, cada um operando em uma camada diferente do modelo OSI.

- **Camada 1 (Física)**: Conexão via fibra óptica conectando o roteador do cliente/parceiro ao roteador da AWS na Direct Connect Location.

- **Camada 2 (Enlace)**: Uso de VLANs (encapsulamento IEEE 802.1Q) para segmentar o tráfego. Cada VLAN é associada a uma Virtual Interface (VIF) específica.

- **Camada 3 (Rede)**: Uso obrigatório do BGP (Border Gateway Protocol) para anúncio e troca de rotas dinâmicas entre o roteador on-premises e a AWS.

## Direct Connect Gateway (DXGW)
- O Direct Connect Gateway age como um roteador global, permitindo que você conecte múltiplas VPCs em diferentes regiões da AWS através de uma única conexão do Direct Connect. 

- Ele é especialmente útil para cenários de interconexão entre regiões, onde você deseja acessar recursos em VPCs localizadas em diferentes regiões da AWS.

## Direct Connect SiteLink

- O Direct Connect SiteLink é um recurso do Direct Connect que **permite o estabelecimento de uma conexão privada entre duas localidades on-premises diferentes**, utilizando a infraestrutura do Direct Connect da AWS.

- Com o SiteLink, o tráfego não chega nem mesmo nas regiões da AWS, passando apenas pelo backbone atráves do Direct Connect Gateway que interliga as duas conexões do Direct Connect.

- O SiteLink é habilitável apenas em VIFs do tipo private e transit, e é útil para cenários de interconexão entre filiais de uma empresa, sem a necessidade de passar pela internet pública ou pelas regiões da AWS.

- A habilitação do SiteLink gera custos adicionais na VIF e é cobrado por hora, além do custo da transferência de dados entre as localidades.

## Link Aggregation Group (LAG)
- Permite agregar múltiplas conexões do Direct Connect em uma única conexão lógica, aumentando a largura de banda e fornecendo redundância.

- Utiliza o protocolo **LACP (Link Aggregation Control Protocol)** para gerenciar a agregação de links.

- Restrições:
  - Todas as conexões agregadas devem ser do mesmo tipo (Dedicated ou Hosted).
  - Todas as conexões físicas precisam usar obrigatoriamente a mesma velocidade (1 Gbps, 10 Gbps, 100 Gbps ou 400 Gbps).
  - As conexões devem estar na mesma direct connect location (mesmo ponto de presença da AWS).
  - O LAG pode ter no máximo 4 conexões agregadas.

## Detectando falhas automaticamente com o BFD (Bidirectional Forwarding Detection)
- O BFD é um protocolo de detecção de falhas de encaminhamento bidirecional, que permite detectar rapidamente falhas em links de rede, incluindo conexões do Direct Connect.

- Sem a utilização do BFD, o BGP pode demorar até 90 segundos para detectar uma falha em um link, o que pode causar interrupções significativas no tráfego de rede.

  - Funciona basicamente como um "ping" entre os roteadores, enviando pacotes de controle em intervalos regulares para verificar se o outro lado da conexão está ativo. Apesar de simples, isso permite detectar falhas em milissegundos, garantindo uma rápida convergência do BGP e minimizando o impacto de falhas na rede.

- O Direct Connect habilita o BFD por padrão em todas as conexões, mas é muito importante verificar se o roteador on-premises também está com o BFD habilitado, isto é o tipo de cenário que pode gerar problemas silenciosos de conectividade caso o BFD esteja habilitado apenas em um dos lados da conexão.

## Criptografando o tráfego do Direct Connect
- O Direct Connect é um serviço de conexão privada, logo, você pensa "pra que criptografar o tráfego se ele nem passa pela internet pública?". Mas existem cenários em que a criptografia é necessária por questão de compliance, segurança ou regulamentação, como em setores financeiros, de saúde ou governamentais.

- A AWS não oferece criptografia nativa para o tráfego do Direct Connect, mas existem algumas alternativas para criptografar o tráfego:
  1. **Criptografia na camada 4-7 (TLS/SSL)**: Utilizando protocolos como HTTPS, FTPS ou outros protocolos que suportem criptografia de ponta a ponta. Essa é a opção mais simples, mas depende de cada aplicação suportar criptografia nativa.

  2. **Criptografia na camada 3 (IPsec)**: Utilizando túneis IPsec sobre o Direct Connect, semelhante ao que é feito no [Site-to-Site VPN](./SiteToSiteVPN.md). Essa opção é mais complexa, mas oferece uma criptografia de ponta a ponta independente da aplicação. 
    - Um detalhe é que o uso do IPSec limitará a largura de banda da conexão, pois o tráfego passa por alto processamento matemático para ser criptografado, no caso do Site-to-Site VPN, o limite de largura de banda é de 1,25 Gbps por túnel.

  3. **Criptografia na camada 2 (MACsec)**: Utilizando o protocolo MACsec (Media Access Control Security) para criptografar o tráfego na camada de enlace. Essa opção é a mais avançada e oferece criptografia de ponta a ponta, mas requer suporte do hardware de rede e configuração adicional.
    - Esse tipo de criptografia é **suportado apenas em conexões do tipo Dedicated Connection**, e não em Hosted Connections. Além disso, o MACsec é suportado apenas em algumas localidades do Direct Connect, então é importante verificar a disponibilidade antes de planejar a implementação.
    - Outro detalhe técnico importante é que **o tráfego não é criptografado de ponta a ponta**, mas sim entre o roteador on-premises e o roteador da AWS na Direct Connect Location. Ou seja, o tráfego ainda passa pelo backbone da AWS sem criptografia, mas com a garantia de que não será interceptado por terceiros durante o transporte.