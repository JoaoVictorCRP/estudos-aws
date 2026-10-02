## Redshift
- O Amazon Redshift é o serviço de data warehouse da Amazon, projetado para a armazenagem de Petabytes de dados de diversas fontes.

- A extração de dados para relatórios de BI ocorre aqui, visto que fazer queries analíticas em um banco de produção poderia causar impactos severos no desempenho do sistema.

- Serviço desenhado para **OLAP (Online Analytical Processing)**, ou seja, análises e consultas complexas em grandes volumes de dados, em vez de operações transacionais típicas de OLTP (Online Transaction Processing), que é o foco de bancos de dados relacionais tradicionais.
  - Para simplificar: OLAP é o processo analítico de dados passados para trazer insights e apoiar a tomada de decisões estratégicas. Enquanto o OLTP foca em operações transacionais em tempo real, como inserções, atualizações e exclusões de registros individuais.

## Características
- **Armazenamento em Colunas**: O Redshift utiliza um armazenamento em colunas, o que significa que dados de cada coluna são armazenados juntos, permitindo uma compressão eficiente e aumentando a velocidade de consultas analíticas que acessam colunas específicas em grandes conjuntos de dados.

- **Consultas Massivamente Paralelas MPP**: distribui as operações de consulta entre múltiplos nós de computação, permitindo a execução simultânea de diversas consultas com alta performance.

- Redshift se integra facilmente com outros serviços da AWS, como Amazon S3, Amazon RDS, Amazon EMR, e Amazon DynamoDB, permitindo a ingestão de dados de várias fontes e simplificando a criação de pipelines de dados.

## A Arquitetura
- O Redshift possui uma arquitetura distribuída composta por um Leader Node e múltiplos Compute Nodes.

- O Leader Node é responsável por gerenciar a comunicação entre os nós de computação e coordenar a execução das consultas.

- Você pode ter de 1 até 128 compute nodes, dependendo do tipo do node.

- Os dados são distribuídos entre os Compute Nodes, permitindo que consultas analíticas sejam processadas em paralelo, aumentando a eficiência e a velocidade de execução.

## Redshift Spectrum
- Permite executar consultas diretamente em dados armazenados no S3 sem a necessidade de carregá-los para o cluster Redshift, proporcionando maior flexibilidade e economia de custos.

- Analogicamente, é similar ao Athena, permitindo consultas SQL diretamente sobre dados armazenados no S3 sem a necessidade de carregá-los para o Redshift.
  - Apesar da semelhança, não confunda: o Redshift Spectrum é uma extensão do Redshift e **depende de um cluster Redshift ativo**, enquanto o Athena é um serviço totalmente gerenciado que não requer cluster. Ademais, o Spectrum é feito para consultar **Petabytes** de dados de forma eficiente, aproveitando a arquitetura distribuída do Redshift.

## Workload Management
- O Redshift possui uma feature chamada Workload Management (WLM), que permite configurar filas de consultas com diferentes prioridades e limites de recursos, garantindo que consultas críticas recebam a atenção necessária sem impactar negativamente outras operações no cluster.

- Com esse recurso você pode, por exemplo, dar prioridade a consultas críticas, garantindo que elas sejam executadas rapidamente, enquanto consultas menos importantes podem ser enfileiradas ou limitadas em termos de recursos.

- É a solução mais simples na hora de lidar com concorrência de consultas no Redshift, pis não demanda alterações significativas na infraestrutura e nem otimização de query.