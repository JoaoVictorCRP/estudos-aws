# API Gateway
Esse é um serviço 100% gerenciado que torna mais fácil o processo de publicação, manutenção e monitoração de APIs em qualquer escala.

## Funcionalidades
### Criação e Gerenciamento de APIs
O API Gateway facilita a criação de APIs para diferentes tipos de aplicativos, como APIs REST, WebSocket ou HTTP. Ele pode ser usado para conectar um frontend com serviços back-end, como Lambda functions, instâncias EC2, ou bancos de dados.

### Integração com outros serviços AWS
O API Gateway integra-se de forma nativa com outros serviços da AWS, como o Lambda, DynamoDB, S3, e CloudWatch, facilitando o desenvolvimento de arquiteturas serverless.

### Throttle e Caching
- **Throttle**: Permite que você controle o tráfego para sua API, <span style="background-color: #e0a800; color: black;font-weight:bold">configurando limites de solicitações por segundo</span> e limites de burst. Isso <span style="background-color: #e0a800; color: black;font-weight:bold">ajuda a proteger seu back-end de sobrecarga e ataques DDoS.</span>

- **Caching**: <span style="background-color: #e0a800; color: black;font-weight:bold">Você pode habilitar o cache em respostas de API</span>, o que melhora a performance e reduz as chamadas para o back-end, economizando custos.

### Segurança e Autenticação
- O API Gateway oferece várias opções de autenticação e autorização para garantir a segurança das APIs, incluindo autenticação via Amazon Cognito, OAuth, AWS IAM roles, e chaves de API.

- **Controle de Acesso**: Também oferece controle de acesso baseado em funções, permitindo que você defina permissões de forma granular para quem pode acessar ou modificar suas APIs.

### Monitoramento e Logging
Amazon CloudWatch: O API Gateway integra-se com o CloudWatch, permitindo monitorar as métricas de uso e performance, como o número de solicitações, erros, e a latência. Além disso, ele permite o uso de logs detalhados para depuração.

### Suporte para WebSockets:
O API Gateway <span style="background-color: #e0a800; color: black;font-weight:bold">permite a criação de APIs WebSocket, que suportam comunicação bidirecional em tempo real</span>, sendo ideal para aplicações como chat online, streaming em tempo real, ou notificações push.

## Configurar uma API Gateway
1. Definir container da API
2. Definir recursos e recursos aninhados (Através de rotas da URL)
3. Para cada recurso:
    - Selecionar o método HTTP suportado
    - Definir medidas de segurança
    - Escolher alvo (Pode ser uma EC2, Lambda, DynamoDB, etc.)

## Anotações
- API Gateway possui baixo custo e escala automaticamente.

- É possível suprimir requisições para prevenir ataques

- Há a opção de suprimir requisições para prevenir ataques DDOS.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Se você</span> utiliza JavaScript/AJAX que <span style="background-color: #e0a800; color: black;font-weight:bold">faz requisições para um servidor externo</span>, onde está sua API Gateway, será necessário ativar o CORS.

