# Amazon MQ

- Na AWS, temos serviços de mensageria como o SQS, SNS e Step Functions, eles no entanto fazem uso do protocolos proprietários da AWS. E a maioria das aplicações utilizam protocolos abertos, como MQTT, AMQP, STOMP, Openwire, WSS, etc.

- Por conta disso, ao migrar para a nuvem, dificilmente é desejado refatorar uma aplicação para utilizar os protocolos da AWS, é pensando nisso que temos o **Amazon MQ**, que ==é um serviço de fila de mensagens gerenciado totalmente compatível com protocolos tradicionais.== Basicamente, estamos falando de um RabbitMQ gerenciado.
## Anotações
- O Amazon MQ roda em servidores (`mq.t3.micro`, `mq.m5.large`, etc), que escalam de maneira limitada (não da mesma forma que o SQS ou SNS, que são serverless).
	- Você pode rodar seus servidores em modo multi-AZ, possibilitando failover.