- Realiza ==**avaliações automáticas de segurança a nível de software**==

### Para Instâncias EC2
- Utiliza o SSM Agent.
- Analisa acessos indesejados de rede.
- Analisa o SO em busca de vulnerabilidades conhecidas.

### Para Imagens no ECR
- Avalia vulnerabilidade nas imagens logo após o push delas para o ECR.

### Para Funções Lambda
- Identifica dependências, bibliotecas e pacotes vulneráveis utilizados na função.

## Os Findings
- Todos os findings e reports do Inspector vão para o Security Hub, além de também possuírem integração com o EventBridge, o que possibilita uma automatização ou envio para o SNS.