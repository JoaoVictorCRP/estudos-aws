# Lambda
O Lambda é um serviço serverless para a execução de funções a partir de um determinado gatilho.

## Como Funciona
### Execução baseada em Eventos
- <span style="background-color: #e0a800; color: black;font-weight:bold">A função é ativada por eventos que podem ser disparados por outros serviços</span> AWS (como S3, DynamoDB, API Gateway, SNS, etc.) ou por fontes externas. Quando o Evento ocorre, o Lambda executa uma função que você definiu para processar os dados do evento

### Código e Funções
- Você escreve funções em linguagens como Python, Node.js, Java, etc. e faz o upload para o Lambda. Cada função tem um único propósito e será invocada quando o evento associado ocorrer.

### Sem Gerenciamento de Infraestrutura
- Não há necessidade de gerenciar servidores, atualizar SOs, ou escalar manualmente a capacidade, tudo isso é gerenciado automaticamente pelo próprio serviço.

### Escalabilidade Automática
- <span style="background-color: #e0a800; color: black;font-weight:bold">O Lambda escala automaticamente com base no número de solicitações recebidas.</span> Se você tem um pico de eventos, o serviço aumenta a capacidade sem precisar de intervenção, e também <span style="background-color: #e0a800; color: black;font-weight:bold">diminui durante períodos de baixa demanda.</span>

## Anotações
- A cobrança é baseada no tempo que a função levou para a execução completa OU no número de requisições (O primeiro milhão de requisições é gratuito, após isso, será cobrado $0,20 por milhão).

- O <span style="background-color: #e0a800; color: black;font-weight:bold">escalonamento</span> do Lambda é <span style="background-color: #e0a800; color: black;font-weight:bold"> horizontal</span>.

- Funções Lambda são independentes, 1 evento = 1 função.

- O AWS X-Ray permite realizar um debug mais apropriado na arquitetura serverless do Lambda.