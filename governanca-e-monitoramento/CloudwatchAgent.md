# CloudWatch Agent

- O CWAgent é um software da AWS feito para coletar métricas que a AWS não coleta nativamente, como número de processos, utilização de memória, syslogs, etc.


## Detalhes

- Anotação para a certificação SOA-C02: Há um plugin para o CWAgent chamado `procstat`, ele permite:

    - Coletar métricas e monitorar sistemas LINUX e WINDOWS.

    - Exemplos de uso: Coleta de tempo de utilização da CPU pelos processos, quantidade de memória utilizada pelos processos, etc.

    - É possível filtrar processos por:
        - `pid` no Linux.
        - `nome.exe` no Windows.

    - Metricas do `procstat` começam com o prefixo `procstat`, exemplo: `procstat\procstat_cpu_time`

- **Você pode coletar métricas customizadas usando os protocolos `StatsD` e/ou o `collectd`**. ==`StatsD` é suportado em ambos Linux e Windows. Já o `collectd` só é suportado no Linux.== Lembre-se disso caso queira coletar dados de uma instância do Windows.