# Métricas de Rede

- Há algumas métricas de rede bem importantes que caem na prova, além dos conhecidos bandwidth, latency e throughput, temos também:

- **Jitter (Oscilação)** : Variação do atraso entre o envio e o recebimento de um pacote entre os dispositivos.

- **PPS (Pacotes por segundo)**: Quantos pacotes são processados por segundos (duh).
  - No geral, essa métrica tem mais a ver com a quantidade de dados que o hardware da máquina receptora consegue processar do que com a qualidade dad rede em si.

- **Maximum Transmission Unit (MTU)**: O maior pacote que pode ser enviado pela rede.
  - O tamanho máximo do pacote depende muito da rede.
  - Tipicamente, o tamanho do pacote (MTU padrão) é 1500 bytes, definição da IEEE.
  - No entanto é possível também enviar pacotes maiores que o valor padrão de 1500 Bytes, estes pacotes são chamados de Jumbo Frames.
    - Os benefícios de usar jumbo frames incluem menor quantidade de pacotes enviados e throughput maior.
    - Alguns roteadores podem não suportar o envio de jumbo frames, o que faz com que o pacote retorne a origem para ser fragmentado e reenviado, ou então ser descartado, causando perda de pacotes (**MTU Black Hole**).
    - O processo de determinar o MTU máximo que pode ser enviado sem fragmentação é chamado de **Path MTU Discovery (PMTUD)**, para que ele funcione, é necessário que o ICMP esteja habilitado na rede, caso contrário, o PMTUD não funcionará e pacotes maiores que o MTU padrão serão descartados.

## Jumbo Frames na AWS

- As VPCs suportam jumbo frames de 9001 bytes para comunicação interna.
  - **O envio de pacotes maiores que 9001 bytes para fora da VPC não é suportado**, e o pacote será descartado silenciosamente.

- Jumbo frames são habilitados por padrão nas VPCs.

- O MTU de VPC emparelhadas inter-regiões é de 8500 bytes.

- O uso de jumbo frames em EC2 em modo cluster (placement group) maximiza o throughput entre as instâncias, e ajuda a alcançar a máxima taxa de transferência entre elas, sendo altamente recomendado pela AWS para workloads de alta performance.

## Definição de MTU em instâncias EC2

- O MTU é definido a nível de ENI, mas também depende do tipo de instância, pois cada tipo de instância tem um tamanho máximo de pacote que pode ser enviado e recebido.

- Você pode verificar o MTU de uma instância EC2 com o comando `ip link show eth0`, e também fazer um **path MTU discovery** com o um endpoint alvo usando o comando `tracepath {nome-do-host}`.

- Para definir o valor do MTU no linux, você pode usar o comando `sudo ip link set dev eth0 mtu {tamanho-do-mtu}`.