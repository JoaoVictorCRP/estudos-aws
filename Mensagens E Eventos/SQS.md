# SQS
É um serviço de mensageria totalmente gerenciado que permite o envio, armazenamento e recebimento de mensagens entre componentes de uma aplicação distribuída sem a necessidade de gerenciar servidores ou infraestrutura.


## Filas de Mensagens
O SQS oferece dois tipos de filas:
- **Standard Queue**: <span style="background-color: #e0a800; color: black;font-weight:bold">Garante entrega de mensagens pelo menos uma vez, mas não mantém a ordem das mensagens.</span> Ideal para sistemas distribuídos que podem lidar com uma possível duplicidade de mensagens. <span style="background-color: green; color: white;font-weight:bold">QUANTIDADE DE TRANSAÇÕES É ILIMITADA</span>


- **FIFO Queue (First In, First Out)**: <span style="background-color: #e0a800; color: black;font-weight:bold">Garante a entrega de mensagens exatamente uma vez e preserva a ordem de envio.</span> Ideal para casos onde a ordem de processamento das mensagens é crítica, como em transações financeiras. <span style="background-color: red; color: black;font-weight:bold">LIMITADA A 300 TRANSAÇÕES POR SEGUNDO.</span>

- **Desacoplamento de Sistemas**: O SQS permite que componentes de uma aplicação se comuniquem sem depender uns dos outros diretamente. <span style="background-color: #e0a800; color: black;font-weight:bold"> Um sistema pode enviar uma mensagem para a fila e continuar seu processamento, enquanto outro sistema pode processar essa mensagem posteriormente, garantindo escalabilidade e tolerância a falhas.</span>


- **Escalabilidade Automática**: O SQS se ajusta automaticamente conforme a demanda aumenta ou diminui, sem necessidade de provisionamento manual de recursos, lidando de maneira eficiente com grandes volumes de mensagens.


- **Mensagens Temporárias**: As mensagens podem ser armazenadas em uma fila por um tempo definido <span style="background-color: #e0a800; color: black;font-weight:bold">(até 14 dias)</span>, dando aos componentes tempo para processá-las. **Se a mensagem não for processada dentro do período, ela expira.**

- **Configuração de Retries (Dead Letter Queues)**: Você pode <span style="background-color: #e0a800; color: black;font-weight:bold">configurar filas de dead-letter para capturar mensagens que falharam no processamento após várias tentativas</span>, facilitando o diagnóstico e correção de problemas sem perda de mensagens.

## Anotações
- No exame, sempre que cair uma questão relacionado ao desacoplamentos (decouple) de aplicações, lembre do SQS, pois eles usam exatamente essa terminologia.

- As mensagens podem pesar até 256KB de texto em qualquer formato

- O S3 é utilizado como ponto de armazenamento das mensagens.

- O SQS é **pull-based**, e não push-based. (É obrigatório ter um puller definido, que na maioria dos casos, é uma instância.)