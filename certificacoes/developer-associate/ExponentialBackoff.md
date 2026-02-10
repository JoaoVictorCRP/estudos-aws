# Exponential Backoff

- Esta é uma estratégia de retry que é muito citada no exame AWS Developer Associate, e é importante entender o conceito por trás dela.

- Se trata de uma **técnica utilizada para lidar com falhas temporárias em sistemas distribuídos**, como serviços da AWS.
  - A ideia é que, quando uma operação falha, em vez de tentar novamente imediatamente, **o sistema espera por um período de tempo que aumenta exponencialmente a cada tentativa subsequente**.

  - Por exemplo, se a primeira tentativa falhar, o sistema pode esperar 1 segundo antes de tentar novamente. Se a segunda tentativa falhar, ele pode esperar 2 segundos, depois 4 segundos, e assim por diante.

- O objetivo do Exponential Backoff é evitar sobrecarregar o sistema com tentativas repetidas em um curto período de tempo, o que pode piorar a situação em caso de falhas temporárias.

- ==Em serviços AWS, essa técnica é recomendada quando precisamos lidar com limites de taxa (rate limites) ou throttling em serviços como API Gateway, DynamoDB, SES==, entre outros.

  - Imagine por exemplo que você está fazendo chamadas para um serviço que tem um limite de 1000 requisições por segundo. Se você ultrapassar esse limite, o serviço pode começar a rejeitar suas requisições. Com o Exponential Backoff, você pode implementar uma lógica que espera um tempo crescente entre as tentativas, reduzindo a chance de atingir o limite novamente.

- **Dica para o exame**: Se você vir uma pergunta sobre como lidar com falhas temporárias ou limites de taxa, a resposta correta provavelmente envolverá o uso de Exponential Backoff.

## Exemplo de Implementação
```python
import time
import random
import boto3
def write_to_dynamo_db(data):
   client = boto3.client('dynamodb')
    if random.random() < 0.5:  # Simula uma falha com 50% de chance
        raise Exception("Falha temporária")
    client.put_item(TableName='MinhaTabela', Item=data)

def exponential_backoff(retries):
    for attempt in range(retries):
        try:
            write_to_dynamo_db({'id': '123', 'value': 'exemplo'})
            print("Operação bem-sucedida")
            return
        except Exception as e:
            wait_time = 2 ** attempt  # Tempo de espera aumenta exponencialmente
            print(f"Falha na tentativa {attempt + 1}: {e}. Aguardando {wait_time} segundos antes de tentar novamente.")
            time.sleep(wait_time)
    print("Todas as tentativas falharam.")

exponential_backoff(5)
```
- Neste exemplo, a função `exponential_backoff` tenta realizar uma operação que pode falhar temporariamente. Se a operação falhar, ela espera um tempo que aumenta exponencialmente antes de tentar novamente, até um máximo de 5 tentativas.