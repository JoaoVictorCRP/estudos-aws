# AWS Site to Site VPN

- O AWS Site to Site VPN é um serviço que permite criar uma conexão segura entre a sua rede on-premises e a AWS, utilizando o protocolo IPsec.

- Ele é utilizado para estender a sua rede local para a nuvem, permitindo que recursos na AWS se comuniquem com recursos na sua rede on-premises de forma segura, como se estivessem na mesma rede local.

- Ele é uma solução ideal para empresas que desejam migrar para a nuvem de forma gradual, mantendo parte da infraestrutura on-premises, ou para aquelas que precisam de uma conexão segura entre diferentes ambientes de rede.

- O AWS Site to Site VPN é altamente disponíivel, provisionando 2 túneis VPN redundantes para cada conexão, garantindo que, caso um túnel falhe, o outro possa assumir a comunicação sem interrupções.

- O limite de largura de banda para cada túnel VPN é de 1,25 Gbps.

## Componentes

- O AWS Site to Site VPN é composto por dois componentes principais:
1. **Customer Gateway (CGW)**: É o dispositivo ou software que representa a sua rede on-premises na AWS. Ele é responsável por estabelecer a conexão VPN com o Virtual Private Gateway (VGW) na AWS.

2. **Virtual Private Gateway (VGW)**: É o dispositivo virtual que representa a AWS na sua rede on-premises. Ele é responsável por receber a conexão VPN do Customer Gateway e rotear o tráfego para os recursos na VPC.

## Propagação de rotas (Estático vs Dinâmico)

- O S2S VPN suporta dois tipos de propagação de rotas:
  - **Estática**: As rotas são configuradas manualmente no Customer Gateway e no Virtual Private Gateway. É mais simples, mas menos flexível, pois se houver um novo range em qualquer um dos lados (AWS ou local), será necessário atualizar as rotas manualmente.

  - **Dinâmica (BGP)**: As rotas são propagadas automaticamente entre o Customer Gateway e o Virtual Private Gateway utilizando o protocolo BGP (Border Gateway Protocol). É mais flexível, pois permite que novas rotas sejam aprendidas automaticamente, sem a necessidade de configuração manual.

- Um detalhe bem importante é que o **route table da AWS não suporta mais que 100 rotas propagadas via BGP, então se você tiver mais de 100 rotas, será necessário utilizar a propagação estática, que por sua vez, possui um limite de 500 rotas**.