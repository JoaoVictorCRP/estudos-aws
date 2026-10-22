## Web Application Firewall (WAF)

- Como o nome diz, o WAF é um firewall a nível de aplicação, ele protege aplicações web contra diversas ameaças e ataques maliciosos comuns.

- É possível especificar diversas condições de bloqueio para requisições, por exemplo:
  - Endereço de IP da origem

  - País de onde a requisição se originou

  - Valores no header

  - Frequência de requisições

  - Strings que aparecem no request body (regex)

  - Tamanho da requisição

  - Presença de código SQL (famoso SQL Injection)

  - Presença de script malicioso (Cross-site scripting)

- O WAF pode ser posicionado em frente a recursos como **CloudFront**, **Application Load Balancer (ALB)** ou **API Gateway**, protegendo-os contra ataques antes que alcancem a aplicação.