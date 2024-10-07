- Este é um serviço mais novo, focado no armazenamento e gerenciamento de segredos.
- Possui a capacidade de forçar a rotação dos segredos a cada X dias.
- A geração do segredo em rotação pode ser automatizada através do Lambda.
- 100% Integrado com o **RDS**, o que o torna **ideal para armazenar senhas de bancos de dados**.
- Segredos podem ser criptografados com KMS.
- <span style="background-color:orange; color:black">Preço : $0.40 por segredo -  valor mensal.</span>
	- <span style="background-color:orange; color:black">Custo adicional: $0.05 a cada 10.000 chamadas de API.</span>
	- Gratuito nos 30 primeiros dias.


## Segredos Multi-region
- É possível realizar a replicação dos segredos em múltiplas regiões AWS.
- O Secrets Manager mantém a sincronia de todas as réplicas com o segredo principal.
- **USE CASES:** Aplicações e BDs multi região e recuperação de desastres.