# 6 R's
Para um processo de migração bem sucedido, a AWS recomenda uma estratégia baseada na consideração dos 6 R's. Vamos entender melhor este conceito.

## Rehosting
- Também conhecido como **"levantar e mudar (Lift-and-shift)"**.
- Envolve mudar a plataforma que hospeda a aplicação sem realizar nenhuma mudança no código ou na lógica dela.
- **Exemplo**: migração de aplicações legado, onde não se pode mexer em nada.

## Replatforming
- Também conhecido como "**levantar, mexer e mudar (lift, tinker and shift)**"
- Aqui se considera uma adaptação nos seus recursos na nuvem para se adequar ao funcionamento da aplicação, mas nada de mexer em código.
- **Exemplo:** Migração de um *MySQL* on-premise para um *Aurora for MySQL.*

## Retiring
- Remoção de recursos desnecessários para a aplicação, promovendo uma migração enxuta e sem falhas.
- **Exemplo:** Remoção de features que não estão mais disponíveis na aplicação, no entanto ainda permanecem nos diretórios ou no próprio código.

## Retain
- Utilizar este conceito para considerar aplicações aposentadas, que ainda estão sendo utilizados somente para recuperar arquivos, fazer queries ou ter exemplos.
- A AWS recomenda não migrar este tipo de aplicação para nuvem, salve seu tempo e seu dinheiro!
- **Exemplo:** Banco de dados com schema antigo.

## Repurchasing
- Pode ser uma boa ideia encerrar o contrato com distribuidores antigos para fazer uma migração completa para a nuvem, considerando uma integração melhor com todos os recursos.
- **Exemplo:** Encerrar um contrato com fornecedor de CRM on premise para comprar um CRM adaptado para a nuvem no AWS Marketplace.

## Refactoring
- Considerado quando você precisa alterar e refatorar código da aplicação, adicionar novas features que só funcionam na nuvem, e não no on premise.
- **Exemplo:** utilizar o SDK da AWS para fazer um sistema que utiliza arquitetura de mensageria através do SQS.