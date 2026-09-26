# Glue
- Serviço gerenciado de extração, transformação e carregamento de dados (ETL).

- Sendo totalmente serverless, ele torna a preparação de dados mais simples, rápida e barata.

- Permite conectar mais de 100 fontes de dados diferentes, facilitando a integração e transformação de dados provenientes de múltiplos sistemas.

## Funcionalidades

- Permite criar, agendar e monitorar fluxos de trabalho de ETL de forma automatizada.

- Descoberta automática de esquemas de dados, permitindo que os dados sejam catalogados e preparados para análise de forma eficiente.

  - A descoberta de esquemas é feita através do **Glue Crawler**, que varre as fontes de dados conectadas, identifica a estrutura dos dados e cria automaticamente tabelas no **Glue Data Catalog**.

  - O **Glue Data Catalog** atua como um repositório centralizado de metadados, permitindo que diferentes serviços da AWS, como Athena e [Redshift](./Redshift.md), acessem e utilizem os dados de forma consistente.


## Componentes Principais
- **Glue Crawler**: Ferramenta que varre as fontes de dados conectadas, identifica a estrutura dos dados e cria automaticamente tabelas no Glue Data Catalog.

- **Glue Data Catalog**: Repositório centralizado de metadados que armazena informações sobre as tabelas e esquemas de dados, permitindo que diferentes serviços da AWS acessem e utilizem os dados de forma consistente.

- **Glue ETL Jobs**: Processos de ETL que extraem dados de diferentes fontes, transformam esses dados conforme necessário e os carregam em destinos apropriados, utilizando o Glue Data Catalog para obter informações sobre os esquemas de dados.

- **Glue DataBrew**: Ferramenta visual de preparação de dados que permite limpar, normalizar e transformar dados de forma interativa, sem a necessidade de escrever qualquer linha decódigo.