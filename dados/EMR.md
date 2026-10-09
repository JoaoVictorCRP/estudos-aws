# Elastic MapReduce
- EMR é um serviço que ==facilita o processo de ETL de grandes volumes de dados, utilizando frameworks como Hadoop, Spark, Flink etc.== 

- Ele permite que você configure clusters de processamento de dados de forma rápida e fácil, escalando de acordo com a demanda, e pagando apenas pelo uso dos recursos.

## Processamento em Escala
- Pode processar PetaBytes de dados de maneira eficiente, utilizando clusters de EC2 que podem ser dimensionados automaticamente conforme a carga de trabalho.

## Integração com o Ecossistema AWS
- Integrado nativamente com outros serviços, como o S3, DynamoDB, RDS, Redshift, e IAM, permitindo fluxos complexos e seguros.

## Custo-Benefício
- Você pode usar instâncias Spot para reduzir os custos do cluster, e ainda configurá-lo para redimensionar automaticamente com base no workload, otimizando os custos.

## Gestão e Automação
- O EMR automatiza muitas tarefas de configuração e gerenciamento do cluster, incluindo provisionamento, configuração de nodos, aplicação de patches de software e monitoramento de desempenho.

## HDFS
- O EMR utiliza o Hadoop Distributed File System (HDFS) para armazenar dados de forma distribuída e redundante, garantindo alta disponibilidade.

- Sendo um sistema de arquivos distribuído, o HDFS divide os dados em blocos e os replica em múltiplos nodos do cluster, garantindo tolerância a falhas e alta disponibilidade.

- Um ponto muito importante é que o ciclo de vida do HDFS está diretamente ligado ao ciclo de vida do cluster. **Quando o cluster é encerrado, todos os dados armazenados no HDFS são perdidos**. 
  - Portanto, é essencial considerar a necessidade de utilizar o S3 para persistência de dados críticos.
