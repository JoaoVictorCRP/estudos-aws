# Glue
- Serviço gerenciado de extração, transformação e carregamento de dados (ETL).

- Sendo totalmente serverless, ele torna a preparação de dados mais simples, rápida e barata.

- Permite conectar mais de 100 fontes de dados diferentes, facilitando a integração e transformação de dados provenientes de múltiplos sistemas.

- Por debaixo dos panos, é uma plataforma Apache Spark. O que o torna totalmente compatível com aplicações e bibliotecas Spark.
  - Isso permite que desenvolvedores aproveitem o ecossistema Spark existente para processar grandes volumes de dados de forma eficiente.

## Funcionalidades

- Permite criar, agendar e monitorar fluxos de trabalho de ETL de forma automatizada.

- Descoberta automática de esquemas de dados, permitindo que os dados sejam catalogados e preparados para análise de forma eficiente.

  - A descoberta de esquemas é feita através do **Glue Crawler**, que varre as fontes de dados conectadas, identifica a estrutura dos dados e cria automaticamente tabelas no **Glue Data Catalog**.

  - O **Glue Data Catalog** atua como um repositório centralizado de metadados, permitindo que diferentes serviços da AWS, como Athena e [Redshift](./Redshift.md), acessem e utilizem os dados de forma consistente.


## Componentes Principais
- **Glue Crawler**: Ferramenta que varre as fontes de dados conectadas, identifica a estrutura dos dados e cria automaticamente tabelas no Glue Data Catalog.

- **Glue Data Catalog**: Repositório centralizado de metadados que armazena informações sobre as tabelas e esquemas de dados, permitindo que diferentes serviços da AWS acessem e utilizem os dados de forma consistente.

- **Glue ETL Jobs**: Processos de ETL que extraem dados de diferentes fontes, transformam esses dados conforme necessário e os carregam em destinos apropriados, utilizando o Glue Data Catalog para obter informações sobre os esquemas de dados.

  - Os Jobs podem ser escritos em Python ou Scala, permitindo flexibilidade na definição das transformações de dados conforme necessário.
  
  - Podem ser baseados em eventos ou agendados para execução periódica, permitindo flexibilidade na automação dos processos de ETL.

  - Você pode provisionar DPUs (Data Processing Units) adicionais para melhorar a performance de execução dos Jobs ETL.
    - Também é possível habilitar métricas para visualizar a capacidade de processamento e o desempenho dos Jobs (==As métricas são visualizadas pelo console do Glue, e não pelo CloudWatch==).

- **Glue DataBrew**: Ferramenta visual de preparação de dados que permite limpar, normalizar e transformar dados de forma interativa, sem a necessidade de escrever qualquer linha decódigo.

## O ETL
- Após a execução dos Jobs ETL, os dados transformados são carregados nos destinos apropriados, prontos para análise ou uso em outros processos.

- Os destinos podem ser um bucket S3, um banco de dados relacional, um data warehouse ou qualquer outro sistema compatível com JDBC.

### Job Bookmarks
- Com os Job Bookmarks, é possível salvar o estado de execução dos Jobs ETL, permitindo que apenas os dados novos (ou modificados) sejam processados nas execuções subsequentes.
  - Isso ajuda a otimizar o desempenho e reduzir o custo de processamento, evitando a reprocessamento de dados que já foram tratados anteriormente.
  - É compatível com as fontes de dados do S3 e de bancos de dados relacionais conectados via JDBC.
    - **Um porém**: em bancos de dados relacionais, os bookmarks só funcionam para processar novas linhas inseridas, não para atualizações ou exclusões de dados existentes.