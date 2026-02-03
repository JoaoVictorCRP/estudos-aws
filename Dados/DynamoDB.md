# DynamoDB
O DynamoDB é um serviço de banco de dados NoSQL projetado para oferecer um desempenho rápido e rapidamente escalável. Ele é o ideal para aplicações que demandam latência mínima.

## Principais Características
- Latência de milisegundos
- Serviço serverless
- Excelente para operações de leitura, você pode inclusive gerenciar a capacidade de leitura de maneira bem simples.
- Pode ser replicado entre regiões.
- ==Multi-AZ por padrão==
- A ==**replicação entre regiões**== não é automática, pois ==precisa ser configurada com Global Tables.==

- ==Itens do DynamoDB podem ter até 400KB de tamanho==, portanto é importante planejar a modelagem dos dados levando isso em consideração.

## Modelagem dos dados
- Como este é um banco não relacional, a organização das tabelas pode inicialmente parecer confusa, mas é bem simples.

- Cada tabela possui **atributos**, que são os equivalentes às colunas em bancos relacionais, e **itens**, que são os equivalentes às linhas.

- **Primary Key:** Diferentemente do modelo relacional, no Dynamo a PK pode ser divida em duas chaves. "Mas como assim... Pode ser?" Pois é, uma dessas chaves é opcional. São elas:
	- **Partition Key**: Identifica um item na tabela, caso você NÃO use uma sort key, a partition key deve ser única.

	- **Sort Key (OPCIONAL):** Utilizada para ordenação de múltiplos itens dentro de uma mesma partição.
    
- **Secondary Indexes:** Permitem consultas adicionais com base em atributos diferentes da chave primária.

    - **Local Secondary Index (LSI):** Compartilha a mesma Partition Key da tabela principal, mas tem uma Sort Key diferente, útil para quando se deseja fazer consultas ordenadas usando um parâmetro diferente da sort key principal.
        - LSIs devem ser criados no momento da criação da tabela.

    - **Global Secondary Index (GSI):** Especifica uma Partition Key e uma Sort Key diferentes da tabela principal, permitindo consultas flexíveis em atributos variados.
        - GSIs podem ser criados a qualquer momento, mesmo após a criação da tabela.

- **Em resumo**: A modelagem dos dados no DynamoDB gira em torno da definição adequada das chaves primárias, enquanto os índices secundários são usados para otimizar as consultas e o desempenho do banco de dados, sendo o **LSI** uma mudança parcial da chave primária (apenas a sort key) e o **GSI** uma mudança completa (partition e sort key).

Veja um Exemplo de tabela no DynamoDB com times do futebol brasileiro:

| ChampionName _(Part. Key)_ | Year (*Sort.Key)* | Championship  | Goals Scored *(GSI - PK)* |
| -------------------------- | ----------------- | ---------------------- | ---------------------- |
| Palmeiras                  | 2016              | Brasileirao            | 73                     |
| Corinthians                | 2015              | Brasileirao            | 66                     |
| Cruzeiro                   | 2014              | Brasileirao            | 68                     |
| Cruzeiro                   | 2013              | Brasileirao            | 74                     |
| Fluminense                 | 2012              | Brasileirao            | 56                     |
| Corinthians                | 2011              | Brasileirao            | 65                     |

### Exemplos de Consultas

- **Buscar todas as temporadas do Palmeiras**:
    - **Partition Key**: `ChampionName = "Palmeiras"`
    - O DynamoDB retornará todos os registros do Palmeiras ordenados pelo ano (Visto que o anoe é a sort key).
    
- **Buscar as temporadas do Corinthians entre 2022 e 2023**:
    - **Partition Key**: `ChampionName = "Corinthians"`
    - **Sort Key**: `Year BETWEEN 1950 AND 2023`
- **Buscar os campeões brasileiros com mais de 70 gols em uma temporada**:
    - **Índice Secundário Global (GSI)**: `Goals Scored > 70`
    - O DynamoDB retornará todos os registros que atendem a esse critério, independentemente do time ou ano.

### Estratégias para modelagem de dados

- **Opção 1**: Utilizar apenas a Partition Key quando os dados forem únicos e não houver necessidades específicas de ordenação, como em um tabela de usuários onde cada usuário tem um ID único `userId`.
    - Neste caso, garanta que a Partition Key seja única para evitar conflitos.
    - Este é o modelo mais simples e direto.

- **Opção 2**: Partition Key + Sort Key (combinação única para cada item), usado para agrupar dados pela partition key e ordenar dentro dessa partição usando a sort key.
    - Exemplo: Em uma tabela de pedidos, a Partition Key pode ser o `userId` e a Sort Key pode ser o `orderDate`, permitindo que você recupere todos os pedidos de um usuário ordenados por data.

## Capacidade Provisionada vs. Capacidade Sob Demanda:
**Provisionada**: Você configura a capacidade de leitura e escrita, e o DynamoDB aloca os recursos necessários para suportar essa carga.

**Sob Demanda**: Você paga apenas pelo que utiliza, o que é ideal para cargas de trabalho imprevisíveis.

## Modelos de Consistência
- Dada a natureza distribuída do DynamoDB, ele oferece dois modelos de consistência para leituras:

- **Leitura Consistente Eventualmente**: Retorna os dados mais recentes, mas sem garantia absoluta de que seja o mais recente.

- **Leitura Fortemente Consistente:** Garante que a leitura sempre retorne os dados mais recentes.
    - Para usar a leitura fortemente consistente, é necessário especificar isso na requisição de leitura.

    - Daí você pensa: "Ora, por que eu não usaria a leitura fortemente consistente sempre?"
        - Porque **a leitura fortemente consistente consome o dobro de RCU (Read Capacity Units)** em comparação com a leitura eventualmente consistente, **deixando a operação mais cara**.

## Read/Write Capacity Units (RCU/WCU)
- No Dynamo, há duas formas de gerenciar a capacidade de leitura e escrita das tabelas: **Provisionada** e **Sob Demanda**.

- **Provisionado**: Quando você escolhe a capacidade provisionada, você define quantas unidades de leitura (RCU) e escrita (WCU) sua tabela pode suportar por segundo.
    
    - **1 RCU**: Representa duas leituras eventualmente consistentes ou uma leitura fortemente consistente **de até 4KB por segundo**.
        - Ou seja, uma leitura fortemente consistente = 1 RCU para até 4KB.
        - Uma leitura eventualmente consistente = 0.5 RCU para até 4KB.
    
    - **1 WCU**: Permite escrever até 1KB de dados por segundo.

- **Sob Demanda**: Nesse modo, você não precisa se preocupar em definir RCU e WCU, pois o DynamoDB ajusta automaticamente a capacidade com base na demanda da aplicação. Você paga apenas pelo que consumir.
    - Esse modo é ideal para aplicações com cargas de trabalho imprevisíveis ou variáveis, porém **pode ser mais caro em cenários de uso constante e elevado**.

### Calculando RCU

- Para calcular o RCU, divida a quantidade de dados (KBs) lidos por segundo pelo tamanho máximo de dados que uma RCU pode ler (4KB), e ajuste conforme o tipo de consistência desejada.

- Exemplo 1: Aplicação quer ler 16KB de dados por segundo com leitura fortemente consistente.
    - Cálculo: 16KB / 4KB = 4 RCU

- Exemplo 2: Aplicação quer ler 23KB de dados por segundo com leitura eventualmente consistente.
    - Cálculo: 23KB (Arredondado para 24KB) / 4KB = 6 RCU / 2 (eventualmente consistente) = 3 RCU

### Excedendo a Capacidade Provisionada
- Se sua aplicação tentar ler ou escrever mais do que a capacidade provisionada, você receberá um erro de `ProvisionedThroughputExceededException`. Para evitar isso, você pode:
    - Aumentar a capacidade provisionada.
    - Implementar uma estratégia de retry com backoff exponencial.
        - Backoff exponencial é uma técnica onde, após cada tentativa falha, o tempo de espera antes da próxima tentativa aumenta exponencialmente, ajudando a reduzir a carga no sistema.

## Nomes das APIs
- A certificação AWS Certified Developer Associate exige que você conheça os nomes das principais APIs do DynamoDB. Aqui estão algumas das mais importantes:

### Escrita
- **PutItem**: Insere um novo item ou substitui um item existente na tabela.
    - Consome WCU com base no tamanho do item.

- **UpdateItem**: Atualiza atributos específicos de um item existente.
    - Consome WCU com base no tamanho dos atributos atualizados.
    - Pode ser usado para implementação de contadores atômicos (atributo numérico que pode ser incrementado ou decrementado sem a necessidade de uma leitura prévia).

### Leitura
- **GetItem**: Recupera um único item da tabela com base na chave primária.
    - Consome RCU com base no tamanho do item.
    - Deve se passar a primary key, que pode ser HASH (Partition Key) ou HASH e RANGE (Partition Key + Sort Key).
    - **Projection Expression** pode ser usada para retornar apenas atributos específicos do item.

- **Query**: Recupera múltiplos itens que compartilham a mesma Partition Key, com opções de filtro e ordenação usando a Sort Key.
    - Consome RCU com base no tamanho dos itens retornados.
    - Permite o uso de filtros adicionais para refinar os resultados.
    - Você pode fazer uma query em uma tabela ou em um índice secundário (GSI ou LSI).

- **Scan**: Examina todos os itens na tabela e retorna aqueles que atendem a critérios específicos.
    - Consome RCU com base no tamanho dos itens retornados.
    - Bem mais caro e lento que o Query, deve ser evitado em tabelas grandes, pois consome muito RCU.
    - Limite o retorno através do uso de `Limit` e `FilterExpression`.


## Conditional Writes
- O DynamoDB possui uma funcionalidade chamada Conditional Writes, que permite que você defina condições específicas para operações de escrita (PutItem, UpdateItem, DeleteItem).

- Você pode, por exemplo, definir que uma atualização só ocorra caso um item não tenha a mesma chave primária, ou que um atributo específico tenha um determinado valor antes de efetuar a escrita.

## DAX (DynamoDB Accelerator)
- O DynamoDB Accelerator é um cache na memória altamente disponível e gerenciado que pode acelerar as leituras do DynamoDB em até 10x, reduzindo a latência para microsegundos, mesmo sob carga elevada.

- **Funcionamento**: armazena em cache os resultados de consultas, leituras de chave-valor e operações de leitura de tabelas do DynamoDB. 
    - Quando uma aplicação faz uma leitura de dados, o DAX verifica primeiro o cache para ver se os dados estão disponíveis. Se os dados não estiverem no cache, o DAX os busca no DynamoDB, armazena no cache, e retorna para a aplicação.

- **Consistência**: Mesmo com o DAX, você pode escolher entre leituras eventualmente ou fortemente consistentes, dependendo de suas necessidades.


## Cross Region Replication (Com o Global Tables)
- O Global Tables do DynamoDB nos dá a opção de replicar um banco em outra região, garantindo maior disponibilidade. Quando se cria uma réplica, deve se especificar qual região você deseja 
criá-la.

- Essa função é bem interessante para que se possa oferecer uma latência baixa para os usuários, independente de qual local do mundo ele está acessando, uma vez que podemos distribuir carga de trabalho entre as réplicas.

- As réplicas são **multi-active**, ou seja, podem ser escritas e lidas em qualquer região onde estejam presentes, a replicação é feita de forma assíncrona entre as regiões.


### DynamoDB Streams
- Permite capturar modificações em **itens** em uma tabela do Dynamo.
    - Conforme destacado, as modificações capturadas são a nível de item, e não de tabela. Caso deseje capturar alterações a nível de tabela, considere o CloudTrail.

- As informações são guardadas por até 24h.

- Informações são em tempo real, possuindo inclusive integração com o Kinesis, Lambda e EventBridge.