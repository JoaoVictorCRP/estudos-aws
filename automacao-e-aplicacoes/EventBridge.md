# EventBridge

- O Amazon EventBridge é um serviço de barramento de eventos serverless que facilita a construção de aplicações orientadas a eventos, permitindo a integração de diversos serviços AWS e aplicações SaaS.

- O nome original deste serviço era **CloudWatch Events**, mas ele foi renomeado para EventBridge para refletir melhor suas capacidades e funcionalidades expandidas.

## Event Buses
- O EventBridge utiliza o conceito de **Event Buses** para organizar e gerenciar os eventos. Existem três tipos principais de Event Buses:
  - **Default Event Bus**: É o barramento de eventos padrão para cada conta AWS, onde os eventos gerados pelos serviços AWS são automaticamente enviados.
  
  - **Custom Event Bus**: Permite criar barramentos de eventos personalizados para aplicações específicas, onde você pode enviar eventos personalizados ou de terceiros.
  
  - **Partner Event Bus**: Utilizado para integrar eventos de parceiros SaaS, como Zendesk, Datadog, etc.

## Regras de Eventos
- As regras de eventos são usadas para filtrar e direcionar os eventos para os destinos apropriados. Você pode criar regras com base em padrões de eventos, permitindo que apenas os eventos que correspondem a determinados critérios sejam processados 
  - Exemplo: apenas eventos do recurso X ou eventos com um valor específico em um campo.

## Destinos de Eventos
- O EventBridge suporta uma ampla variedade de destinos para onde os eventos podem ser enviados, incluindo:
  - AWS Lambda
  - Amazon SNS
  - Amazon SQS
  - Step Functions
  - Kinesis Data Streams
  - Um endpoint HTTPS para integração com aplicações externas, através da feature **API Destinations**.
  - E muitos outros serviços AWS e parceiros SaaS.

## Integração Multiconta
- O EventBridge permite a integração entre contas AWS, permitindo que eventos de uma conta sejam enviados para outra conta, facilitando a construção de arquiteturas distribuídas e a comunicação entre diferentes ambientes.

- Para isto, é necessário configurar permissões adequadas para permitir que as contas se comuniquem e compartilhem eventos de forma segura.

  - A configuração deve ser feita no Event Bus de destino, onde você precisa adicionar uma política de permissão que permita que a conta de origem envie eventos para o barramento de eventos do destino.

- Essa funcionalidade é especialmente útil para organizações que gerenciam múltiplas contas AWS e desejam centralizar o monitoramento e a resposta a eventos em um único local.