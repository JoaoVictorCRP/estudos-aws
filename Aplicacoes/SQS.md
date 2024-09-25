# SQS
É um serviço de mensageria totalmente gerenciado que permite o envio, armazenamento e recebimento de mensagens entre componentes de uma aplicação distribuída sem a necessidade de gerenciar servidores ou infraestrutura.


## Filas de Mensagens
O SQS oferece dois tipos de filas:
- **Standard Queue**: Garante entrega de mensagens pelo menos uma vez, mas não mantém a ordem das mensagens. Ideal para sistemas distribuídos que podem lidar com uma possível duplicidade de mensagens. <span style="background-color: green; color: white;font-weight:bold">   QUANTIDADE DE TRANSAÇÕES É ILIMITADA
</span>

- **FIFO Queue (First In, First Out)**: Garante a entrega de mensagens exatamente uma vez e preserva a ordem de envio. Ideal para casos onde a ordem de processamento das mensagens é crítica, como em transações financeiras. <span style="background-color: red; color: black;font-weight:bold">LIMITADA A 300 TRANSAÇÕES POR SEGUNDO.</span>

## **Desacoplamento de Sistemas**
O SQS permite que componentes de uma aplicação se comuniquem sem depender uns dos outros diretamente. Um sistema pode enviar uma mensagem para a fila e continuar seu processamento, enquanto outro sistema pode processar essa mensagem posteriormente, o nome técnico disso é notificação pull.

## **Escalabilidade Automática**
O SQS se ajusta automaticamente conforme a demanda aumenta ou diminui, sem necessidade de provisionamento manual de recursos, lidando de maneira eficiente com grandes volumes de mensagens.

## **Mensagens Temporárias**
As mensagens podem ser armazenadas em uma fila por um tempo definido **(até 14 dias)**, dando aos componentes tempo para processá-las. Se a mensagem não for processada dentro do período, ela expira.

## **Configuração de Retries (Dead Letter Queues)**
Você pode configurar filas de dead-letter para capturar mensagens que falharam no processamento após várias tentativas, facilitando o diagnóstico e correção de problemas sem perda de mensagens.

## Anotações
- No exame, sempre que cair uma questão relacionado ao desacoplamentos (decouple) de aplicações, lembre do SQS, pois eles usam exatamente essa terminologia.

- As mensagens podem pesar até 256KB de texto em qualquer formato.

- Por baixo do panos, o S3 é utilizado como ponto de armazenamento das mensagens.

- O SQS é **pull-based**, e não push-based. (É obrigatório ter um puller definido, que na maioria das vezes, é um outro componente ou camada da aplicação.)