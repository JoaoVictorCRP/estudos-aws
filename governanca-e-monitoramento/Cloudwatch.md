# Cloudwatch

- O Cloudwatch é um serviço de Monitoramento e observabilidade da AWS.

- Ele coleta dados de logs, métricas e eventos de diversos serviços AWS, aplicações on-premises e recursos de nuvem de terceiros.

- Com esses dados, o Cloudwatch permite monitorar o desempenho, a integridade e a disponibilidade dos recursos e aplicações.

## Cloudwatch Cross-Account Observability

- O Cloudwatch Cross-Account Observability é um ==recurso que permite monitorar e visualizar métricas, logs e alarmes de várias contas AWS em um único painel de controle==.

- Isso é especialmente útil para organizações que gerenciam várias contas AWS, pois facilita a centralização do monitoramento e a identificação de problemas em diferentes ambientes.

- Com o Cross-Account Observability, é possível configurar uma conta central de monitoramento que coleta dados de outras contas AWS, permitindo uma visão unificada do desempenho e da integridade dos recursos em toda a organização.

## Canary Synthetics
- O Canary Synthetics é um recurso do Cloudwatch que permite criar e gerenciar canários, que são scripts automatizados que simulam o comportamento dos usuários em aplicações web.

- É muito útil para monitorar a disponibilidade e o desempenho de aplicações web, APIs e endpoints, garantindo que eles estejam funcionando corretamente para os usuários finais.

## Custom Metrics
- Você pode criar métricas personalizadas no Cloudwatch para monitorar aspectos específicos do seu ambiente ou aplicação que não são cobertos pelas métricas padrão fornecidas pelos serviços AWS.

- As métricas personalizadas podem ser criadas a partir de dados de logs usando Log Metric Filters, ou podem ser enviadas diretamente para o Cloudwatch usando a API `PutMetricData`.

- Ao criar uma métrica personalizada você pode definir se ela será uma métrica de **High Resolution** (granularidade de 1 segundo) ou de **Standard Resolution** (granularidade de 1 minuto), dependendo das necessidades de monitoramento da sua aplicação.
  - **Observação**: As métricas coletadas pela própria AWS, por padrão, são SR, mas é possível configurar algumas métricas para serem HR, caso seja necessário um monitoramento mais detalhado. Isso é feito através do Detailed Monitoring, que pode ser habilitado para serviços como EC2, RDS, etc.

## Cloudwatch Logs
- O Cloudwatch Logs é um serviço que permite coletar, monitorar e armazenar logs de aplicações, sistemas operacionais e serviços AWS.

- Com o Cloudwatch Logs, é possível centralizar os logs de diferentes fontes, facilitando a análise e a identificação de problemas.

- Ele oferece recursos como criação de grupos de logs, streams de logs, filtros de métricas e alarmes, permitindo monitorar o desempenho e a integridade das aplicações e sistemas.

### Log Metric Filters
- Os **Log Metric Filters são usados para extrair métricas específicas dos logs** coletados pelo Cloudwatch Logs.

- Com eles, é possível definir padrões de pesquisa nos logs e criar métricas personalizadas com base nesses padrões.

  - Por exemplo, a ocorrência da palavra `ERROR` em um log de aplicação.
  
  - Ao identificar o padrão, ele incrementa uma métrica personalizada, que pode ser monitorada através de um gráfico/dashboard e/ou usada para acionar alarmes.

### Log Subscription Filters
- Os **Log Subscription Filters permitem enviar logs do Cloudwatch Logs para outros serviços da AWS ou destinos externos em tempo real** (Data streaming).

- Destinos suportados incluem:
  - AWS Lambda
  - Amazon Kinesis Data Streams
  - Amazon Kinesis Data Firehose
  - Serviços de terceiros via Amazon EventBridge

- Caso de uso comum: enviar logs para um cluster OpenSearch para buscas e análises avançadas, ou para um bucket S3 para arquivamento e análises futuras.

