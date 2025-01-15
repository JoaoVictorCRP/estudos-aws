Aqui estão anotações referentes a segurança de redes na AWS.

## Network Reachability Analyzer
- Opção dentro do console VPC que ==nos permite traçar o caminho (*path*) que um recurso da AWS faz até o outro dentro da rede.==

- Aqui você pode definir um IP de origem e outro de destino para verificar se estes estão se comunicando corretamente, ou se há algum empecilho.

## Traffic Mirroring
- Ideal para ==inspecionar pacotes de rede para solução de problemas na infraestrutura==.

- **Como Usar**: Você deve configurar uma ferramenta de monitoramento em uma instância, como o _Wireshark_, por exemplo. Daí ==você deve **habilitar o traffic mirroring na VPC** para que você possa copiar dados de tráfego de uma *ENI (Elastic Network Interface)* e enviá-los para outra==.

