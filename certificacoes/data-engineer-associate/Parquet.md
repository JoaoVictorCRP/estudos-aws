# Apache Parquet

- O Apache Parque é um formato de armazenamento de dados colunar, otimizado para leitura e escrita eficiente de grandes volumes de dados.

- Diferentemente do CSV, que é um formato de armazenamento baseado em linhas, o Parquet organiza tudo em colunas, permitindo leituras mais rápidas e granularidade na seleção de dados.

- Ele é amplamente utilizado em ecossistemas de big data, como Apache Hadoop, Apache Spark e AWS Glue, devido à sua eficiência e compatibilidade com diferentes ferramentas de processamento de dados.

- Um arquivo parquet "cru" não é legível diretamente por humanos, pois é armazenado em um formato binário otimizado para desempenho, e não em texto simples como CSV.
  
  - Um exemplo de arquivo Parquet pode ser encontrado no arquivo `sample-simple.parquet`, no diretório dessa anotação. Para ler ele, você pode utilizar a extensão `parquet-viewer`, do Visual Studio Code.

- Sempre que se deseja otimizar a performance de um processo de leitura e escrita de grandes volumes de dados, o uso do formato Parquet é altamente recomendado.
  
  - Na prova da certificação, é importante ter em mente a priorização desse formato, especialmente em comparação ao CSV. 
  
  - Muitas questões abordam a transformação de dados de CSV para Parquet para otimização de performance, através do Glue ou funções Lambda.