O Step Functions é um serviço gerenciado que nos permite orquestrar múltiplos serviços da AWS em fluxos de trabalho com controle de execução, falha e dependência de etapas.

Ele é muito útil para criar **processos complexos com lógica condicional** sem precisar codificar toda a lógica de controle da aplicação.

---
## Como funciona?
- A orquestração dos serviços baseia-se em diagramas de **máquina de estado**, que são definidos em formato JSON usando o [Amazon States Language (ASL)](https://states-language.net/spec.html#states-fields).
	
- As fases de um workflow são chamados **steps**, um step pode ser integrados a:
	- Lambdas
	- Jobs no ECS, Batch ou EMR
	- Serviços como SQS, DynamoDB, SageMaker, SNS.
	- Outras step functions
	- Chamadas para APIs HTTP

---
## Tipos de Execução (Standard vs Express)
- No Step Functions podemos executar um workflow de duas formas: **Standard** ou **Express**, veja a tabela com as diferenças abaixo:

| Tipo                     | **Standard Workflows** 🚚                                  | **Express Workflows** 🚀                               |
| ------------------------ | ---------------------------------------------------------- | ------------------------------------------------------ |
| **Uso**                  | ==Processos de longa duração== (minutos, horas, dias)      | Altamente escalável e rápido (milissegundos a minutos) |
| **Duração máx.**         | Até **1 ano** de execução                                  | Até **5 minutos**                                      |
| **Throughput**           | Até 2.000 execuções por segundo                            | Até 100.000 execuções por segundo                      |
| **Custo**                | Por **transição de estado**                                | Por **duração + número de execuções**                  |
| **Exemplos**             | Fluxos ETL, processamento de pedidos, workflows com espera | Processamento de eventos, pipelines em tempo real      |
| **Retries, logs, audit** | Completo, detalhado, com histórico                         | Limitado, logs devem ser enviados ao CloudWatch        |

---
## Tipos de Workflows (Sync vs. Assync)

### 🔄 **Synchronous Workflows**
- A execução **retorna o resultado imediatamente** para quem chamou.
- Suportado com **StartSyncExecution** para **Express Workflows**. 
- Ideal quando um cliente (ex: API Gateway) precisa da **resposta final do fluxo** na mesma requisição.
    
📌 Exemplo:
> Uma API REST chama um Express Workflow via API Gateway e quer retornar o resultado da execução diretamente ao usuário.

### 🕓 **Asynchronous Workflows**

- Execução é disparada, mas o cliente **não espera a resposta final**.
- Pode usar **eventos de callback**, **SQS**, **EventBridge**, ou armazenar estados em banco (como DynamoDB) até que a execução termine.

📌 Exemplo:
> Uma Lambda ou EventBridge dispara o fluxo, que executa por minutos ou horas (ex: transcoding de vídeo, processo de aprovação com espera).