## Redshift
- O Amazon Redshift é o serviço de data warehouse da Amazon, projetado para a armazenagem de Petabytes de dados de diversas fontes.

- A extração de dados para relatórios de BI ocorre aqui, visto que fazer queries analíticas em um banco de produção poderia causar impactos severos no desempenho do sistema.

- Serviço desenhado para **OLAP (Online Analytical Processing)**, ou seja, análises e consultas complexas em grandes volumes de dados, em vez de operações transacionais típicas de OLTP (Online Transaction Processing), que é o foco de bancos de dados relacionais tradicionais.
  - Para simplificar: OLAP é o processo analítico de dados passados para trazer insights e apoiar a tomada de decisões estratégicas. Enquanto o OLTP foca em operações transacionais em tempo real, como inserções, atualizações e exclusões de registros individuais.

## Características
- **Armazenamento em Colunas**: O Redshift utiliza um armazenamento em colunas, o que significa que dados de cada coluna são armazenados juntos, permitindo uma compressão eficiente e aumentando a velocidade de consultas analíticas que acessam colunas específicas em grandes conjuntos de dados.

- **Consultas Massivamente Paralelas MPP**: distribui as operações de consulta entre múltiplos nós de computação, permitindo a execução simultânea de diversas consultas com alta performance.

- Redshift se integra facilmente com outros serviços da AWS, como Amazon S3, Amazon RDS, Amazon EMR, e Amazon DynamoDB, permitindo a ingestão de dados de várias fontes e simplificando a criação de pipelines de dados.

## Durabilidade
- O Redshift faz replicação dentro do cluster, garantindo que os dados sejam duplicados entre os nós de computação. Isso aumenta a durabilidade e a disponibilidade dos dados, protegendo contra falhas de hardware.

- Snapshots são gerados automaticamente pelo Redshift e podem ser usados para restaurar o cluster a um estado anterior.
  - O período de retenção padrão é de 1 dia, mas pode ser ajustado para até 35 dias (obviamente, quanto maior o período de retenção, maior o custo associado).

- Além disso, o Redshift também faz backups períodicos automáticos no Amazon S3, garantindo que os dados possam ser recuperados mesmo em caso de falhas catastróficas no cluster.

- Nodes que apresentarem falhas são substituídos automaticamente, garantindo a continuidade do serviço sem perda de dados.

## A Arquitetura
- O Redshift possui uma arquitetura distribuída composta por um Leader Node e múltiplos Compute Nodes.

- O Leader Node é responsável por gerenciar a comunicação entre os nós de computação e coordenar a execução das consultas.

- Você pode ter de 1 até 128 compute nodes, dependendo do tipo do node.

- Os dados são distribuídos entre os Compute Nodes, permitindo que consultas analíticas sejam processadas em paralelo, aumentando a eficiência e a velocidade de execução.

## Importando / Exportando Dados

- O Redshift permite importar dados de diversas fontes, como arquivos CSV, JSON, Avro, Parquet e ORC armazenados no Amazon S3, além de suportar integração com o AWS Data Pipeline e o AWS Glue para ETL.

- Para a importação de dados, o Redshift oferece o comando **`COPY`**, que permite carregar grandes volumes de dados de forma eficiente e paralelizada a partir de fontes externas, como o S3, DynamoDB, hosts remotos (via SSH) e outros bancos de dados **compatíveis com JDBC**.

- Para exportar dados, podemos usar o comando **`UNLOAD`**, que permite gravar os resultados de consultas SQL diretamente no S3 em formatos como CSV, Parquet e JSON, facilitando a integração com outros serviços e pipelines de dados.

- Se você habilitar a feature **Enhanced VPC Routing**, todo o tráfego de rede entre o Redshift e outras fontes de dados externas passará pela VPC (ou ao menos preferirá a rota pela VPC), aumentando a segurança e o controle sobre o tráfego de dados.

- Também temos features que permitem a cópia automática de dados de uma fonte na AWS para o Redshift. Algumas delas são:
  - **Auto-copy from S3**, que permite que o Redshift copie automaticamente dados de arquivos recém-carregados no S3 para tabelas do Redshift, simplificando o processo de ingestão de dados.
  - O **Aurora zero-ETL integration**, para o Aurora, que permite a ingestão automática de dados no Aurora para o Redshift sem a necessidade de processos ETL manuais.
  - E o **Redshift Streaming Ingestion**, que permite a ingestão contínua de dados em tempo real no Redshift a partir de fontes de streaming, como o Amazon Kinesis Data Streams e o MSK (Amazon Managed Streaming for Apache Kafka).

- Se você quer copiar dados que já estão no Redshift para uma outra tabela dentro do mesmo cluster, você pode usar o comando **`INSERT INTO ... SELECT ...`**, que permite inserir dados em uma tabela a partir do resultado de uma consulta em outra tabela.

## Vacuum
- O comando **`VACUUM`** no Redshift é usado para reorganizar tabelas e recuperar espaço de armazenamento após operações de **DELETE** ou **UPDATE**.
- Ele ajuda a manter a performance das consultas, garantindo que os dados estejam fisicamente organizados de forma eficiente.
- Existem diferentes tipos de **VACUUM**, temos: 
  - **FULL** (padrão), que reorganiza completamente a tabela e recupera espaço de armazenamento.
  - **SORT ONLY**, que apenas reorganiza os dados de acordo com a chave de ordenação, sem recuperar espaço.
  - **DELETE ONLY**, que remove linhas marcadas para exclusão e recupera espaço, sem reorganizar os dados existentes.
  - **REINDEX**, que recria os índices da tabela para melhorar a performance das consultas, sem reorganizar os dados ou recuperar espaço.

## Redshift Spectrum
- Permite executar consultas diretamente em dados armazenados no S3 sem a necessidade de carregá-los para o cluster Redshift, proporcionando maior flexibilidade e economia de custos.

- Analogicamente, é similar ao Athena, permitindo consultas SQL diretamente sobre dados armazenados no S3 sem a necessidade de carregá-los para o Redshift.
  - Apesar da semelhança, não confunda: o Redshift Spectrum é uma extensão do Redshift e **depende de um cluster Redshift ativo**, enquanto o Athena é um serviço totalmente gerenciado que não requer cluster. Ademais, o Spectrum é feito para consultar **Petabytes** de dados de forma eficiente, aproveitando a arquitetura distribuída do Redshift.

## Workload Management
- O Redshift possui uma feature chamada **Workload Management (WLM)**, que permite configurar filas de consultas com diferentes prioridades e limites de recursos, garantindo que consultas críticas recebam a atenção necessária sem impactar negativamente outras operações no cluster.

- Com esse recurso você pode, por exemplo, dar prioridade a consultas críticas, garantindo que elas sejam executadas rapidamente, enquanto consultas menos importantes podem ser enfileiradas ou limitadas em termos de recursos.

- É a solução mais simples na hora de lidar com concorrência de consultas no Redshift, pois não demanda alterações significativas na infraestrutura e nem otimização de query.

- O WLM pode ser gerenciado de forma **manual**, onde você configura filas e recursos explicitamente, ou de forma **automática**, onde o Redshift ajusta dinamicamente os recursos com base na carga de trabalho.

## Escalabilidade concorrente
- O Redshift permite escalar tanto o armazenamento quanto o poder de processamento de forma independente.

- Isso é feito através de recursos como **Concurrency Scaling** e **Elastic Resize**, que garantem que o cluster consiga lidar com picos de carga e grandes volumes de dados sem comprometer a performance.
  - A escalabilidade é virtualmente ilimitada, permitindo que o Redshift se adapte a diferentes cargas de trabalho e volumes de dados sem necessidade de reconfiguração manual do cluster.

- É possível usar o WLM para gerenciar quais consultas irão para o **Concurrency Scaling**, garantindo que consultas críticas tenham acesso a recursos adicionais durante picos de carga, enquanto consultas menos prioritárias podem ser enfileiradas ou limitadas.