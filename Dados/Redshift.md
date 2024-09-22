## Redshift
O Amazon Redshift é o serviço de data warehouse da Amazon, projetado para a armazenagem de Petabytes de dados de diversas fontes, a extração de dados para relatórios de BI ocorre aqui, já que fazer queries de extração em um banco de produção seria um workload bem grande, né?

### Características
- **Armazenamento em Colunas**: O Redshift utiliza um armazenamento em colunas, o que significa que dados de cada coluna são armazenados juntos, permitindo uma compressão eficiente e aumentando a velocidade de consultas analíticas que acessam colunas específicas em grandes conjuntos de dados.
- **Consultas Massivamente Paralelas MPP**: distribui as operações de consulta entre múltiplos nós de computação, permitindo a execução simultânea de diversas consultas 
com alta performance.

- Redshift se integra facilmente com outros serviços da AWS, como 
Amazon S3, Amazon RDS, Amazon EMR, e Amazon DynamoDB, 
permitindo a ingestão de dados de várias fontes e simplificando a 
criação de pipelines de dados.

### Redshift Spectrum:
- Permite executar consultas diretamente em dados armazenados no S3 sem a necessidade de carregá-los para o cluster Redshift, 
proporcionando maior flexibilidade e economia de custos.

**Um detalhe importante é que o Redshift é disponibilizado em apenas 2 Availability Zones**