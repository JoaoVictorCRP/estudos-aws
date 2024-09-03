# VPC

## O que é?
O **Virtual Private Cloud** é o serviço de rede privada virtual da AWS. Ele permite ter controle total da infraestrutura de rede em nuvem,
nele se tem controle total do ambiente virtual, incluindo selecção da sua própria faixa de IP, criação de subredes e configuração da tabela de roteamento e gateways de rede.

Isto permite que você provisione uma seção lógicamente isolada da nuvem AWS, onde é possível utilizar recursos utilizando desta rede.
<span style="background-color: #e0a800; color: black;font-weight:bold">
    Podemos, por exemplo, criar uma sub-rede de acesso público para o frontend da aplicação e outra sub-rede privada para o backend.
</span>

É possível definir várias camadas de segurança, incluindo security groups e ACLs, o que ajuda muito no controle de acesso à instância em cada subrede.

<span style="background-color: #e0a800; color: black;font-weight:bold">
    Além de tudo, também é possível criar uma extensão da sua rede local através de uma VPN site-to-site ou pelo AWS Direct Connect.
</span>

![Estrutura de rede com VPC](estruturaVPC.png)


## Detalhes
### VPC Padrão vs VPC Customizada
- VPCs padrão são user-friendly, permitindo dar um deploy imediato.

- Todas as subredes na VPC padrão possuem saída para a internet habilitada.

### VPC Peering
- Permite que você conecte uma VPC a outra através de um roteamento direto utilizando os IPs privados.
- Instâncias se comportam como se estivessem na mesma rede privada.
- <span style="background-color: #e0a800; color: black;font-weight:bold">Você pode emparelhar VPCs com outra conta AWS</span>, assim como também pode fazer isso com outras VPCs da sua conta.

- <span style="background-color: #e0a800; color: black;font-weight:bold">
    É possível emparelhar VPCs em regiões diferentes.
</span> 
- O emparelhamento é em estrela, isto é, 1 VPC central pareando com outras 4. Sem emparelhamento transitivo.

## Reserva de IPs
- Ao criar uma subrede, você irá notar que <span style="background-color: #e0a800; color: black;font-weight:bold">5 IPs já estarão reservados</span>, exemplificando em uma rede 10.0.0.0/24 a reserva é feita desta forma:
    - 10.0.0.0 => Endereço da rede;
    - 10.0.0.1 => Reservado para o roteador VPC;
    - 10.0.0.2 => Reservado para o servidor DNS (sempre é o range da rede + 2);
    - 10.0.0.3 => Reservado para uso futuro (serviços que poderão ser usados no futuro);
    - 10.0.0.255 => Reservado para o broadcast.

## Criação de Subredes
- Quando você criar uma VPC, também será criado uma Route Table, uma Network Access Control List (NACL) e um Security Group, todos com permissões padrão. Resumidamente, as permissões são:
    - **Route Table**: Inicialmente sem acesso à internet.
    - **NACL**: Permite todo o tráfego Inbound e Outbound.
    - **Security Group**: Bloqueia todo o tráfego Inbound (exceto entre instâncias no mesmo grupo) e permite todo o tráfego Outbound.

- <span style="color: red;font-weight:bold">ATENÇÃO: Por padrão, o auto-assign de IP público fica desativado ao criar uma nova subrede.</span> 

## Diferença entre Route Table, NACL e Security Group
### **1. Route Table** 👑
- <span style="background-color: green;font-weight:bold">Função:</span> Determinar como o tráfego é roteado dentro da VPC. Ela define o encaminhamento com base no endereço de destino da solicitação, permitindo direcionar o tráfeco para gateways, subredes e outras VPCs.
- <span style="background-color: purple;font-weight:bold">Use Case:</span> Controlar a comunicação entre subredes e definir rotas de saída para internet ou outras redes privadas.

### 2. Network ACL 👮
- <span style="background-color: green;font-weight:bold">Função:</span> Listas de controle que operam 
<span style="background-color: #e0a800; color: black;font-weight:bold">NO NÍVEL DA SUBREDE.</span>
 São stateless, portanto você deve configurar as regras de entrada e de saída separadamente.

- <span style="background-color: purple;font-weight:bold">Use Case:</span> Implementada para aplicar regras de segurança adicionais **NAS SUBREDES**, como <span style="background-color: #e0a800; color: black;font-weight:bold">em um ambiente onde você precisa bloquear todo o tráfego de entrada de um intervalo de IP específico, mas permitir o tráfego de saída.</span>

### 3. Security Group 🤓
- <span style="background-color: green;font-weight:bold">Função:</span> São firewalls no <span style="background-color: #e0a800; color: black;font-weight:bold">NÍVEL DA INSTÂNCIA</span>, controlando o tráfego de entrada e saída para instâncias EC2 específicas. Eles **são stateful**, o que significa que uma regra de entrada ou saída automaticamente permite o tráfego de retorno correspondente.

- <span style="background-color: purple;font-weight:bold">Use Case:</span> Usados para proteger instâncias específicas, como em um cenário onde você deseja permitir o tráfego SSH (porta 22) de um determinado IP externo, mas bloquear todo o tráfego de entrada de outras portas.

## VPC Flow Logs
- Essa é uma ferramenta que <span style="background-color: #e0a800; color: black;font-weight:bold">permite capturar informações do tráfico IP de entrada e saída da sua VPC</span>. Os dados do Flow log são armazenados no **CloudWatch Logs** ou, **opcionalmente, em um Bucket S3**. Após ter criado um flow log, você poderá analisá-lo em detalhes nos logs da CloudWatch.

- Os Flow logs podem ser criados em três níveis:
    - VPC
    - Subrede
    - Interface de Rede da instância

- NÃO é possível definir um flow log de uma VPC emparelhada cross-account.

## Bastion Host
Um Bastion Host é um servidor que atua como um ponto de acesso seguro para administrar intância que ficam em subredes privadas da VPC, o Bastion é o único a estar localizado na rede pública e ser exporto à internet. Adms acessam o Bastion Host via SSH ou RDP e, a partir dele, conectam-se às instâncias privadas, que não tem acesso à internet.

### Observações:
- Um NAT Gateway ou NAT instance é usada para providenciar tráfego da intenet para instâncias em subredes privadas.
- Um Bastion é usado para administrar instâncias de maneira segura.
- NÃO É POSSÍVEL UTILIZAR UM NOAT GATEWAY COMO BASTION.

## Network Address Translation (NAT)
O NAT é uma técnica usada para traduzir endereços IP privados de uma rede interna para endereços IP públicos (ou outros endereços IPs) para tráfego de saída ou de entrada. No contexto da AWS, o NAT é usado para permitir que instâncias em sub-redes privadas da VPC possam acessar a internet ou outros serviços externos, sem que seu IP privado seja exposto.

### NAT Gateway
- Serviço gerenciado que permite que instâncias em sub-redes privadas enviem tráfego de saída para a internet, enquanto impede conexões de entrada iniciadas da internet.
- São altamente disponíveis e <span style="background-color: #e0a800; color: black;font-weight:bold">escalam automaticamente para lidar com grandes volumes de tráfego. (vão de 5Gbps até 45Gbps) </span>
- O uso de um NAT Gateway gera custos com base no tempo de execução (por hora) e na quantidade de dados processados.
- Redundante em uma AZ.
- Não é associado a nenhum security group.
- Recebe um endereço de IP público automaticamente.

### NAT Instance
- É possível usar uma instância EC2 configurada com um software NAT para servir a mesma função que o NAT Gateway. A vantagem é o controle total sobre a configuração, mas isso requer gerenciamento manual, incluindo ajustes para alta disponibilidade e escalabilidade

- É uma opção de custo menor que o NAT gateway, mas 
<span style="background-color: #e0a800; color: black;font-weight:bold">só é ideal para pequenas cargas, pois uma maior carga de trabalho exigirá mais poder de processamento da instância NAT, além do fato de que o trabalho de configuração será 100% manual.</span>

- Há um recurso nas instância EC2 chamado Source/Destination, que faz com que a instância "cheque" se ela é a origem ou o destino de qualquer tráfego enviado ou recebido na rede. 
<span style="background-color: #e0a800; color: black;font-weight:bold">
No caso das NAT Instances, esse recurso PRECISA ESTAR DESABILITADO, uma vez que essa instância deverá lidar com tráfego onde ela não é origem e nem destino. 
</span> 

## Network ACL
- <span style="background-color: #e0a800; color: black;font-weight:bold">Regras do NACL são obedecidas em ordem cronológica</span> (Portanto se eu tenho uma regra de aceitar tudo na ordem 100, e uma regra de DENY para o IP x.x.x.x na ordem 200, o IP x.x.x.x não será banido, pois a regra 100 triunfou sobre a regra 200).
- É muito importante liberar o acesso inbound/outbound das portas efêmeras, o range das portas efêmeras variam de acordo com o cliente que você está se comunicando. Mas no geral são as portas 1024-65535, portanto libere estas. Veja a documentação:
![Portas Efêmeras](portasEfemeras.png)

- Ao criar um novo NACL, todo o tráfego estará com regra de DENY por padrão.

- Um NACL pode estar associado a múltiplas subredes, no entanto uma subrede só pode esta associado a um único NACL.

## AWS Direct Connect
Este é um serviço que <span style="background-color: #e0a800; color: black;font-weight:bold">estabelece uma conexão dedicada entre sua infraestrutura local e a AWS</span>. Diferente de uma conexão padrão à internet, o Direct Connect proporciona uma conexão com alta largura de banda, baixa latência, e com mais consistência, uma vez que não depende da internet pública.

- Útil para um carga pesada de throughput.
- Oferece uma conexão estável e segura, uma vez que não utiliza a internet pública para transferência de dados entre sua rede e a AWS.

### Passos para configurar um Direct Connect
- **1.** Crie uma interface virtual na seção Direct Connect do Console. (**PUBLIC VIRTUAL INTERFACE**)
- **2.** Vá para a seção de VPC > VPN, e então crie um Customer Gateway.
- **3.** Crie uma Vpg (Virtual Private Gateway)
- **4.** Acople a VPG na VPC desejada
- **5.** Vá no painel de "Conexões VPN" e crie uma nova conexão VPN.
- **6.** Selecione a VPG e o customer gateway nas opções da VPN.
- **7.** Assim que a VPN estiver disponível, vá até o customer gateway nopainel do direct connect e configure a VPN.

Vídeo de como configurar: https://www.youtube.com/watch?v=QRRmSvu-Ozs

## Global Accelerator
O Global Accelerator é um serviço de rede que melhora a disponibilidade e a performance das suas aplicações. Com ele, o tráfego dos usuários é roteado para a poderosa rede backbone da Amazon, e apartir dela, segue para várias regiões da AWS, escolhendo automaticamente a melhor rota para minimizar a latência.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Ideal para aplicações que atendem usuários distribuídos globalmente</span>, como sites, APIs, e serviços em tempo real.

- Por padrão, <span style="background-color: #e0a800; color: black;font-weight:bold">o GA providencia dois IPs estáticos que estarão associados ao seu accelerator</span>.

- É possível diminuir ou aumentar a porcentagem do tráfego para um determinado endpoint group ajustando o traffic dial nas configurações.

![Global Accelerator](globalAccelerator.png)

## VPC Endpoints
Permitem que você conecte sua VPC a serviços da AWS de forma privada, sem a necessidade de usar a internet, gateways, NAT ou VPNS. Eles <span style="background-color: #e0a800; color: black;font-weight:bold">proporcionam uma maneira segura e eficiente de acessar serviços AWS diretamente da sua VPC, mantendo o tráfego dentro da rede da AWS.</span>

### Tipos de VPC Endpoint:
- Interface Endpoints
    - Utiliza uma Elastic Network Interface (ENI) com endereço IP privado dentro da VPC. Esse endpoint é conectado aos serviços AWS, como o S3, DynamoDB e outros que suportam a interface VPC.
    - Ele é ideal para se conectar a serviços baseados em IP, como o S3, Cloudwatch, SNS e outros.
    - O tráfego nunca sai da rede privada da AWS.

- Gateway Endpoints
    - d

    ![alt text](image.png)
## Anotações
- 1 Subrede = 1 Availability Zone.

- O tamanho máximo de uma VPC é /16 (16 bits reservados para rede), que permite 65.536 dispositivos.
- Você só pode ter uma IGW (Internet Gateway) por VPC.

- <span style="background-color: #e0a800; color: black;font-weight:bold"> As AZs são ordenadas aleatoriamente para cada conta da AWS</span>, por exemplo: O SP-EAST-1A da minha conta não é o mesmo que o SP-EAST-1A na sua conta, até porque se não fosse aleatório todo mundo sempre iria escolher as AZs A e B.

- Nenhuma subrede é criada automaticamente.

- Você só pode ter 1 Internet Gateway por VPC.

- Security Groups não abrangem VPCs.

- O bloqueio de IPs deve ser feito pelo NACL, e não pelos Security Groups.

- O protocolo que permite o ping é o ICMP.

- <span style="background-color: #e0a800; color: black;font-weight:bold">É possível fazer com que uma NAT Instance tenha HA</span>, no entanto isso exigirá um Autoscaling Group, subredes em diferentes AZs e um script que automatize o failover.

- <span style="background-color: red; color: black;font-weight:bold"> Ao acessar uma instância Y apartir de uma instância X, não se esqueça de dar um chmod 400 no arquivo de keypair.