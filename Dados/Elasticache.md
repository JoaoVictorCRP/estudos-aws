- Elasticache é o serviço que fornece a opção de armazenar dados e operações em memória cache, dessa forma salvando o tempo de processamento e garantindo uma velocidade excepcional para a aplicação ou para as consultas realizadas em um banco de dados.

- Neste serviço temos duas opções de sistema: Redis e Memcached, ambos custam o mesmo preço - desde que comparados com especificações idênticas, claro. - no entanto  possuem algumas sutis diferenças:

## Redis
- ==Utilize o Redis se você deseja montar uma operação mais complexa.==
- Suporta uma variedade bem grande de tipos de dados.
- Possui replicação e alta persistência nativamente.
- ==Possui suporte para dados geoespaciais.==
___
### Memcached
- ==Muito usado em aplicações mais simples.==
- NÃO tem suporte para snapshots, replicação ou estruturas de dados mais avançadas.
- ==Possui arquitetura Multithreaded== que garante uma excelente performance para caches básicos.