# VPC Flow Logs
- O VPC Flow Log é uma ferramenta de monitoramento do tráfego de rede que entra e sai das interfaces de rede (ENIs) em uma VPC. 

- Ele permite capturar informações detalhadas sobre o tráfego, como endereços IP de origem e destino, portas, protocolos e ações (permitido ou negado).

- É a principal ferramenta de auditoria no que se diz respeito a segurança de redes, pois permite identificar padrões de tráfego suspeitos, ataques e problemas de conectividade.

- Ele é utilizado pelo GuardDuty para monitorar comunicações suspeitas de componentes da VPC com serviços externos.

- É importante ressaltar que o VPC Flow Log não captura o conteúdo do tráfego, apenas os metadados. Portanto ele não é uma ferramenta de sniffing de pacotes, mas sim de monitoramento e auditoria.