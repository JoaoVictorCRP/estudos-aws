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
o Kinesis é a plataforma de Streaming Data da AWS. Ele ==torna mais fácil o processo de carregamento e análise destes dados==, permitindo que se possa construir uma aplicação customizada para necessidades específicas acerca dos dados.

## Componentes
### Kinesis Data Streams
- **Função**: Coletar e armazenar grandes volumes de dados em tempo real. Os dados são enviados para streams, que podem ser lidos e processados continuamente por consumidores, como aplicativos ou funções AWS Lambda.

- **Exemplo de Uso**: Capturar e armazenar logs de servidor, dados de redes sociais, ou cliques de sites para análise em tempo real.
    
#### Shards
- Os *shards* são a unidade básica de capacidade para o streaming de dados. Cada *shard* em um stream pode capturar, armazenar e processar dados.
- A capacidade dos shards é gerenciável de duas formas:
	- **Modo provisionado**: Você pode aumentar ou diminuir manualmente a quantidade de shards conforme sua necessidade.
	
	- **Modo on-demand**: Não é necessário provisionar ou gerenciar capacidade, escabilidade automático baseado no thoughput dos últimos 30 dias.

#### Funcionamento dos Shards
- **Divisão de Dados**: ==Quando você envia dados para um stream, cada registro é atribuído a um shard específico com base em uma partition key.== Isso permite que diferentes shards processem dados simultaneamente, dividindo a carga entre eles.

- **Gravação**: Cada *shard* pode lidar com até 1MB de dados por segundo ou 1.000 registros por segundo para gravações.

- **Leitura**: Cada *shard* pode fornecer até 2 MB de dados para leitura e 5 leituras por segundo.

#### Enhanced Fanout
- Permite que o KDS tenha diversas aplicações consumidoras para receber dados, reduzindo o lag ocorrido em cenários onde existem diversos consumidores lendo de uma mesma data stream. Esta é uma feature criada especialmente para lidar com problemas de performance com múltiplos consumidores.

___
### Kinesis Data Firehose
- **Função**: ==Enviar os dados capturados diretamente para serviços== como Amazon S3, Redshift, OpenSearch, ou Splunk. Ele é totalmente gerenciado, não exigindo a criação de streams ou o gerenciamento de consumidores.

- **Exemplo de Uso**: Enviar logs de dados para um bucket S3 ou indexá-los diretamente no OpenSearch para consultas em tempo real.
---
### Kinesis Data Analytics
- **Função**: ==Processar e analisar dados em tempo real usando consultas SQL==. Isso permite transformar, filtrar e agregar dados imediatamente à medida que são recebidos no Kinesis Data Streams ou Firehose.
- **Exemplo de Uso**: Analisar os cliques de uma campanha publicitária em tempo real e identificar padrões de comportamento.

---
### Kinesis Video Streams
- **Função**: Capturar e armazenar streams de mídia. Ele criptografa e indexa dados de vídeo de streams e permite acessar estes dados por meio de APIs fáceis de usar.
- **Exemplo de uso**: Criação de aplicações com visão computacional (integrado ao *Amazon Rekognition Video*) Reprodução de mídia ao vivo para navegadores com o  recurso de HLS (HTTP Live Streaming)

---
## Anotações
- Se o volume de dados ou a frequência de eventos ultrapassa a capacidade de um único shard, você pode adicionar shards para aumentar a capacidade do stream. (==Escalabilidade é horizontal==)

- O período de retenção de dados do Data Streams é ajustável: **de 24h até 365 dias**.

- No modelo Firehose, ==não há persistência direta de dados.==

- Para utilização do HLS para stream de video, é necessário primeiro criar uma sessão de streaming utilizando a API **GetHLSStreamingSessionURL**, que retorna um token para acessar a sessão HLS.

- O envio de dados com o Kinesis Data Streams é feito pelo KPL (Kinesis Producer Library), mas também pode ser realizado pelo **Kinesis Agent**, que é um software que coleta dados do server (de maneira similar ao CWAgent) e os envia na stream.