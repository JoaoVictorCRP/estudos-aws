# SWF
O Simple Workflow Service é um serviço web que torna mais fácil o trabalho coordenado distribuído entre os componentes de uma aplicação. 
Ele possui vários casos de uso, como o processamento de mídia, backend de aplicações web e pipeline de dados.

## Workers e Deciders

- **Workers**: São responsáveis por executar as tarefas do fluxo de trabalho. <span style="background-color: #e0a800; color: black;font-weight:bold">Eles podem ser sistemas automatizados ou humanos.</span>

- **Deciders**: São responsáveis por coordenar o fluxo de trabalho, determinando quais tarefas devem ser executadas em seguida com base nos resultados anteriores.

## Execução de Longa Duração:

- O SWF pode gerenciar fluxos de trabalho com duração de segundos a meses. Isso é especialmente útil para processos que exigem múltiplas etapas ou que dependem de ações externas que podem demorar para serem concluídas, como validação de documentos ou aprovação manual.


## SWF vs SQS
- <span style="background-color: #e0a800; color: black;font-weight:bold">A execução de um workflow no SWF pode levar até um ano</span>, enquanto que no SQS leva 14 dias para a expiração de uma mensagem.

- SWF é orientado a tarefas, enquanto que o SQS é orientado a mensagens.

- <span style="background-color: #e0a800; color: black;font-weight:bold">SWF geralmente é utilizado em contextos onde a ação manual de um ser humano é envolvida</span>, já o SQS é a comunicação entre componentes lógicos de uma aplicação