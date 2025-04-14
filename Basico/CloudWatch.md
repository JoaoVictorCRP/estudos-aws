O CloudWatch é o serviço utilizado para monitoramento das métricas dos recursos na AWS.

## O Agent
O CW Agent pode ser utilizado para coletar métricas personalizadas da instância EC2, como syslogs, uso de disco e uso de memória. (Estas que não são coletadas nativamente pela AWS).

- **Você pode coletar métricas customizadas usando os protocolos `StatsD` e/ou o `collectd`**. ==`StatsD` é suportado em ambos servidores Linux e Windows. Já o `collectd` só é suportado no Linux. ==Lembre-se disso caso queira coletar dados de uma instância do Windows.
