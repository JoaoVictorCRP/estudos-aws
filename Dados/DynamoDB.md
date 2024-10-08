## DynamoDB
O DynamoDB é um serviço de banco de dados NoSQL projetado para oferecer um desempenho rápido e rapidamente escalável. Ele é o ideal para aplicações que demandam latência mínima.
___
### Capacidade Provisionada vs. Capacidade Sob Demanda:
**Provisionada**: Você configura a capacidade de leitura e escrita, e o DynamoDB aloca os recursos necessários para suportar essa carga.

**Sob Demanda**: Você paga apenas pelo que utiliza, o que é ideal para cargas de trabalho imprevisíveis.
___
### Modelos de Consistência:
**Leitura Consistente Eventualmente**: Retorna os dados mais recentes, mas sem garantia absoluta de que seja o mais recente.<br><br>
**Leitura Fortemente Consistente:** Garante que a leitura sempre retorne os dados mais recentes. (É uma opção mais cara que a consistência eventual, mas bem interessante dependendo do caso de uso).
___
### DAX (DynamoDB Accelerator):
O DynamoDB Accelerator é um cache na memória altamente disponível e gerenciado que pode acelerar as leituras do DynamoDB em até 10x, reduzindo a latência para microsegundos, mesmo sob carga elevada.<br><br>
**Funcionamento**: armazena em cache os resultados de consultas, leituras de chave-valor e operações de leitura de tabelas do DynamoDB. Quando uma aplicação faz uma leitura de dados, o DAX verifica primeiro o cache para ver se os dados estão disponíveis. Se os dados não estiverem no cache, o DAX os busca no DynamoDB, armazena no cache, e retorna para a aplicação.<br><br>
**Consistência**: Mesmo com o DAX, você pode escolher entre leituras consistentes eventualmente ou fortemente consistentes, dependendo de suas necessidades. <br><br>
___
### Cross Region Replication (Com o Global Tables)
O Global Tables do DynamoDB nos dá a opção de replicar um banco em outra região, garantindo maior disponibilidade. Quando se cria uma réplica, deve se especificar qual região você deseja 
criá-la.<br>
Essa função é bem interessante para que se possa oferecer uma latência baixa para os usuários, independente de qual local do mundo ele está acessando, uma vez que podemos distribuir carga de trabalho entre as réplicas.
