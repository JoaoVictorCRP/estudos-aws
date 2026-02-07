# X-Ray

- O Amazon X-Ray é um serviço utilizado para traçar o fluxo de trabalho das suas aplicações na AWS e como elas se interconectam, **tudo de maneira visual** e detalhada, por meio de gráficos e mapas de dependências.

- Abaixo temos um grafo exibido pelo X-Ray, mostrando como os serviços estão interconectados:
![X-Ray Diagram](images/x-ray-diagram.png)

- Ele é ==especialmente útil quando precisamos depurar e identificar gargalos em aplicações distribuídas== (microsserviços). Se o exame falar sobre troubleshooting de aplicações distribuída, então a resposta vai estar relacionada ao X-Ray.

- Serviços compatíveis:
	- **Lambda**
		- Ao usar o X-Ray em uma Lambda, é necessário habilitar o **active tracing** na configuração da função.
	- **Instâncias EC2 (ou servidores on-premises)** - Via SDK ou agente do X-Ray.
	- **ECS**
	- **Elastic Beanstalk**
	- **API Gateway**

## Casos de Uso
- Identificar gargalos em aplicações distribuídas.
- Analisar as dependências entre os serviços.
- Descobrir a causa raiz de erros e gargalos de desempenho.
- Identificar usuários que estão sendo impactados por erros ou lentidão.

## Tracing
- O X-Ray utiliza o conceito de **tracing** para coletar dados sobre as solicitações que passam por suas aplicações. Ele gera um **trace** para cada solicitação, que é composto por **segments** e **subsegments**.
	- **Segment**: Representa uma unidade de trabalho, como uma solicitação HTTP ou uma chamada a um banco de dados.
	
	- **Subsegment**: Representa uma parte específica do trabalho, como uma consulta SQL ou uma chamada a outro serviço.

- Você pode adicionar annotations e metadata aos seus traces para facilitar a análise e a identificação de problemas, estes funcionam como tags e chaves-valor, respectivamente.

## Como usar o X-Ray
- Há duas maneiras principais de usar o X-Ray:
	1. **SDK do X-Ray**: Você pode instrumentar seu código usando o SDK para coletar dados de tracing. Ele está disponível para várias linguagens de programação, como Java, Python, Node, etc.
	
	2. **Daemon do X-Ray**: Para aplicações que não podem ser instrumentadas diretamente, você pode usar o Daemon do X-Ray para coletar dados de tracing. O agente é um processo que roda em segundo plano e coleta dados de tracing de suas aplicações através da interceptação de chamadas de rede.
		- Neste caso, é importante que o host onde o agente está rodando tenha as permissões necessárias para enviar dados para o X-Ray.