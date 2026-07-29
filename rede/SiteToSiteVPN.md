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

## O Roteamento transitivo do Site to Site VPN
- **O Virtual Private Gateway (VGW) NÃO suporta roteamento transitivo**. Se a sua rede local se conecta a uma VPC por meio de uma VPN terminada em um VGW, esse VGW só dá acesso aos recursos internos daquela VPC específica.

- **VPN + VPC Peering**: O tráfego da rede local não consegue atravessar a VPC A para chegar à VPC B via VPC Peering. O VPC Peering não é transtivo naturalmente.

- Sobre sair para a internet via AWS a partir de uma rede local:
  - O VGW NÃO encaminha tráfego vindo da rede local para a Internet (seja via IGW, NAT Gateway ou NAT Instance). O tráfego de saída da rede local para a internet deve sair pela própria conexão de internet do on-premises.

  - Se precisar centralizar a saída de internet na AWS: Deve-se substituir o VGW pelo [Transit Gateway (TGW)](./TransitGateway.md) e criar uma Egress VPC dedicada.

- Acesso a Gateway Endpoints (S3 e DynamoDB):
  - NÃO funciona via VGW. Gateway Endpoints são alvos na tabela de rotas e não possuem ENIs/IPs privados na VPC, impedindo o roteamento a partir da VPN.

- Acesso a Interface Endpoints (AWS PrivateLink):
  - FUNCIONA perfeitamente. Como o Interface Endpoint aloca uma ENI com IP privado na VPC, o tráfego da rede local atravessa o VGW normalmente rumo a esse IP.

## DPD - Dead Peer Detection
- O DPD é um mecanismo utilizado para detectar se o peer (o outro lado da conexão VPN) está ativo ou não. Ele funciona enviando mensagens de keepalive periodicamente (`R-U-THERE`) para o peer e aguardando uma resposta.

- Se o peer não responder 3 keepalives consecutivos, o DPD considera que o peer está inativo e encerra a conexão VPN. Isso permite que o outro túnel VPN redundante assuma a comunicação sem interrupções.

- Por padrão, o valor do timeout do DPD é de 30 segundos, porém isso é ajustável.

- Os túneis podem também ser terminados devido a inativdade. Você pode configurar o tempo de inatividade que deseja, ou então configurar um host para mandar ICMP (ping) periodicamente para manter o túnel ativo.

- Você pode configurar as seguintes ações para o timeout do DPD:
  - **Clear (Padrão)**: Encerra a sessão e remove todas as rotas aprendidas via BGP.
  - **None**: Mantém a sessão e as rotas ativas, mesmo se o peer parar de responder.
  - **Restart**: Tenta renegociar uma nova sessão como o peer imediatamente.

## Os dois túneis VPN redundantes

- Como já foi dito, o Site-to-Site VPN sempre provisiona dois túneis IPsec redundantes para cada conexão, terminando em duas zonas de disponibilidade (AZs) diferentes do lado da AWS.

- Existem duas estratégias de Utilização, são elas:

- **Ativo / Ativo**:
  - Ambos os túneis permanecem UP simultaneamente.

  - Roteamento Estático ou Dinâmico (BGP): No roteamento estático, o tráfego de saída da AWS usará apenas um túnel. Com BGP, é possível enviar e receber tráfego por ambos os túneis.

  - Roteamento Assimétrico: No modo Ativo/Ativo, o tráfego de ida pode sair por um túnel e a volta entrar pelo outro. Se houver firewalls stateful no meio, isso causará drop de pacotes.

  - Como mitigar assimetria com BGP:

  - **Para o tráfego AWS -> On-Premises**: Utilize AS Path Prepending na sessão BGP do túnel secundário para forçar a AWS a preferir o túnel primário.

  - **Para o tráfego On-Premises -> AWS**: Ajuste a Local Preference no seu dispositivo on-premises (CGW) para preferir o túnel primário.

- **Ativo / Passivo**:

  - Um túnel carrega todo o tráfego enquanto o outro fica em modo Standby.

  - É a configuração padrão caso você use roteamento estático no VGW ou configure métricas/prioridades BGP para favorecer um único caminho.

  - Failover: Se o túnel ativo cair, a alternância para o túnel standby ocorre automaticamente via BGP (geralmente levando alguns segundos até a convergência dos keepalives do DPD e do BGP).