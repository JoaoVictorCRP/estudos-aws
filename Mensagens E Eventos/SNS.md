# SNS
O SNS trabalha em um modelo pub/sub através dos tópicos, um tópico é o canal de comunicação entre publisher e subscriber.

Todo tópico tem um publisher e N subscribers, quando o publisher envia a mensagem, ela chegará direito para o seus subscribers.

Os subscribers podem ser servidores web, emails e também endpoints, como:
- Funções Lambda
- Filas SQS
- Webhooks
 
Além disso, o SNS também pode ser utilizado para enviar notificações direto para seus usuários finais, através de notificações push em seus dispositivos, emails