- Este é um serviço mais novo, focado no armazenamento e gerenciamento de segredos.
- ==Possui a capacidade de forçar a rotação dos segredos a cada X dias.==
- ==A geração do segredo em rotação pode ser automatizada através do Lambda.==
- 100% Integrado com o **RDS**, o que o torna **ideal para armazenar senhas de bancos de dados**.
- Segredos podem ser criptografados com KMS.
- ==Preço : $0.40 por segredo -  valor mensal.==
	- ==Custo adicional: $0.05 a cada 10.000 chamadas de API.==
	- Gratuito nos 30 primeiros dias.


## Segredos Multi-region
- É possível realizar a replicação dos segredos em múltiplas regiões AWS.
- O Secrets Manager mantém a sincronia de todas as réplicas com o segredo principal.
- **USE CASES:** Aplicações e BDs multi região e recuperação de desastres.

## Single e Multi-User rotation (RDS)
#### Single-User Rotation
- **Definição**: Estratégia em que as **mesmas credenciais armazenadas no Secret** são usadas para realizar a rotação.

- **Como funciona**:
    - O AWS Secrets Manager utiliza as credenciais armazenadas no Secret atual para executar as etapas de rotação.
    - Durante a rotação, ele altera a senha do usuário no banco de dados e atualiza o Secret para refletir essa nova senha.

- Simples de configurar e gerenciar.
- Durante o processo de rotação, pode haver um breve período de interrupção caso o segredo seja usado por uma aplicação enquanto a senha está sendo atualizada.

#### Multi-User Rotation
- **Definição**: Estratégia em que o ==Secrets Manager cria um **clone do usuário do banco de dados** para realizar a rotação, utilizando-o temporariamente.==

- **Como funciona**:
    1. Um **usuário auxiliar (clone)** é criado no banco de dados com as mesmas permissões do usuário original.
    2. O Secrets Manager usa esse usuário auxiliar para alterar a senha do usuário principal.
    3. Após a rotação, o Secret é atualizado com a nova senha, e o clone pode ser removido (dependendo da configuração).

- Minimiza a interrupção da aplicação, pois o usuário original continua operacional durante o processo.
- ==**É ideal para cenários onde a alta disponibilidade é crítica.**==

- **Limitações**:
    - Requer mais configurações no banco de dados (criação de permissões para o clone).
    - Pode ser mais complexo de implementar em ambientes que não suportam múltiplos usuários facilmente.