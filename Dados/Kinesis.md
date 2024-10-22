# Kinesis
Para entender o Kinesis, primeiro precisamos saber a definição de *Streaming Data*:

## O que é Streaming Data?
**São dados gerados de maneira contínua**, originados de milhares de fontes diferentes, as quais tipicamente enviam os dados de maneira simultânea em pequenos pacotes (Kilobytes). Exemplo:
- Compras em grandes lojas online
- Preço das ações
- Dados de jogos (Especialmente jogos multiplayer)
- Dados de redes sociais
- Dados geoespaciais (Uber)
- IOT

## Funcionalidades
Certo, o <span style="background-color: #e0a800; color: black;font-weight:bold">Amazon Kinesis é a plataforma de Streaming Data da AWS.</span> Ele <span style="background-color: #e0a800; color: black;font-weight:bold">torna mais fácil o processo de carregamento e análise destes dados</span>, permitindo que se possa construir uma aplicação customizada para necessidades específicas acerca dos dados.

## Componentes
### Kinesis Data Streams
- **Função**: Coleta e armazena grandes volumes de dados em tempo real. Os dados são enviados para streams, que podem ser lidos e processados continuamente por consumidores, como aplicativos ou funções AWS Lambda.

- **Exemplo de Uso**: Capturar e armazenar logs de servidor, dados de redes sociais, ou cliques de sites para análise em tempo real.
    
    #### Shards
	- Os *shards* são a unidade básica de capacidade para o streaming de dados. Cada *shard* em um stream pode capturar, armazenar e processar dados, e **você pode aumentar ou diminuir a quantidade de shards conforme a necessidade de processamento e volume de dados**. 

    #### Funcionamento dos Shards
    - **Divisão de Dados**: ==Quando você envia dados para um stream, cada registro é atribuído a um shard específico com base em uma partition key. ==Isso permite que diferentes shards processem dados simultaneamente, dividindo a carga entre eles.

    - **Gravação**: Cada *shard* pode lidar com até 1MB de dados por segundo ou 1.000 registros por segundo para gravações.

    - **Leitura**: Cada *shard* pode fornecer até 2 MB de dados para leitura e 5 leituras por segundo.



### Kinesis Data Firehose
- **Função**: <span style="background-color: #e0a800; color: black;font-weight:bold">Envia os dados capturados diretamente para serviços</span> como Amazon S3, Redshift, Elasticsearch, ou Splunk. Ele é totalmente gerenciado, não exigindo a criação de streams ou o gerenciamento de consumidores.

- **Exemplo de Uso**: Enviar logs de dados para um bucket S3 ou indexá-los diretamente no Elasticsearch para consultas em tempo real.

### Kinesis Data Analytics
- **Função**: <span style="background-color: #e0a800; color: black;font-weight:bold">Processa e analisa dados em tempo real usando consultas SQL</span>. Isso permite transformar, filtrar e agregar dados imediatamente à medida que são recebidos no Kinesis Data Streams ou Firehose.
- **Exemplo de Uso**: Analisar os cliques de uma campanha publicitária em tempo real e identificar padrões de comportamento.

## Anotações
- Se o volume de dados ou a frequência de eventos ultrapassa a capacidade de um único shard, você pode adicionar shards para aumentar a capacidade do stream. (<span style="background-color: #e0a800; color: black;font-weight:bold">Escalabilidade é horizontal</span>)

- No modelo de Data Streams, <span style="background-color: #e0a800; color: black;font-weight:bold">os shards armazenam dados de 24h até 7 dias</span>, dependendo da sua escolha.

- No modelo Firehose, <span style="background-color: #e0a800; color: black;font-weight:bold">não há persistência direta de dados.</span>