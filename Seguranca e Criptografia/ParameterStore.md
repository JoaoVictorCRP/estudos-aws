- O Parameter Store é um sub serviço do Systems Manager, utilizado para armazenar variáveis de ambiente e dados de acesso sensíveis que são utilizados no código de uma aplicação.

- Oferece criptografia integrada com KMS

- Suporta versionamento dos parâmetros.

- **Notificações facilmente integráveis com o EventBridge.**

- Integração com CloudFormation.

- É possível agrupar parâmetros sob um prefixo (diretório)

## <span style="background-color:blue; color:white">Tiers</span>
### Standard (Grátis)
- 4KB de tamanho máximo.
- Até 10,000 parâmetros.

### Advanced ($0.05 por mês pra cada parâmetro)
- 8KB de tamanho máximo.
- Até 100,000 parâmetros.
- Permite definir configurações adicionais com o **Parameters Policies**.


## <span style="background-color:blue; color:white">Parameters Policies</span>
- Oferece a opção de definir uma data de expiração para parâmetros, o que forçará atualização ou deleção de dados sensíveis.
- Um parâmetro pode ter várias policies associadas.
- Notificações configuráveis:
	- Expiração.
	- Expiração está próxima.
	- "Mudanças não ocorrem há x dias."