# SNS
O SNS trabalha em um modelo pub/sub através dos tópicos, um tópico é o canal de comunicação entre publisher e subscriber.

Todo tópico tem um publisher e N subscribers, quando o publisher envia a mensagem, ela chegará direito para o seus subscribers.

Os subscribers podem ser servidores web, emails e também endpoints, como:
- Funções Lambda
- Filas SQS
- Webhooks
 
Além disso, o SNS também pode ser utilizado para enviar notificações direto para seus usuários finais, através de notificações push em seus dispositivos, emails

## Message Filtering
Através do SNS também é possível filtrar mensagens. Isso ocorre através de um JSON que validará os atributos.

> Suponhamos, por exemplo, que o nosso chefe queira receber um email toda vez que uma instância for desligada, já o supervisor quer receber um email quando a instância for ligada.  

Podemos então fazer um evento que notifique uma mudança de estado da instância, e então no tópico SNS nós filtramos: 
- Se o estado for "*stopping*", mande email para o chefe. 
- Se o estado for "*starting*", mande email para o supervisor.
- Se não, ignore.