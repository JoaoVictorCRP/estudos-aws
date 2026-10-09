# JDBC vs ODBC

- Ambas são interfaces de programação que permitem a comunicação de aplicações com bancos de dados.

- O Java Database Connectivity (JDBC) é uma API específica para Java que permite a comunicação de aplicações Java com bancos de dados relacionais.
  - O JDBC se integra diretamente com o ecossistema Java, e só é compatível com aplicações Java (ou outras que utilizam a JVM, como o Kotlin e o Scala).

- O Open Database Connectivity (ODBC) é uma API mais genérica, que permite a comunicação de aplicações com diferentes tipos de bancos de dados, **independentemente da linguagem de programação utilizada**.
  - ODBC foi desenvolvido para ser independente de plataforma e linguagem, isso permite que diferentes ambientes se conectem a diversos bancos de dados de forma padronizada.

  - Apesar de ser independente de plataforma e linguagem, o ODBC é fortemente acomplado ao Windows, sendo historicamente mais utilizado em ambientes Windows (Não atoa, pois o ODBC foi desenvolvido pela Microsoft).
    - Existem implementações que possibilitam a utilização em sistemas operacionais como Linux e macOS, embora o suporte e a popularidade sejam menores em comparação ao Windows.

- Em resumo, o JDBC é ideal para aplicações Java que precisam se conectar a bancos de dados relacionais, enquanto o ODBC oferece uma solução mais genérica e multiplataforma, adequada para diferentes linguagens e tipos de bancos de dados.