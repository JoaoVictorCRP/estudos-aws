# 7 R's
Para um processo de migração bem sucedido, a AWS recomenda uma estratégia baseada na consideração dos 7 R's. Vamos entender melhor este conceito.

## Relocating
- Estratégia baseada em mover a aplicação para a nuvem em um downtime mínimo

- Nenhuma alteração no código ou arquitetura da aplicação deve ser realizada.

## Rehosting
- Também conhecido como "**levantar e mudar (lift and shift)**"

- Envolve mudar a plataforma que hospeda a aplicação sem realizar nenhuma mudança no código ou na lógica dela.

- **Exemplo**: migração de aplicações legado, onde obrigatoriamente não se mexe em nada do código.

## Replatforming
- Também conhecido como "**levantar, mexer e mudar (lift, tinker and shift)**"

- Aqui se considera uma adaptação nos seus recursos na nuvem para se adequar ao funcionamento da aplicação, mas nada de mexer em código.

- **Exemplo:** Migração de um *MySQL* on-premise para um *Aurora for MySQL.*

## Repurchasing
- Pode ser uma boa ideia encerrar o contrato com distribuidores antigos para fazer uma migração completa para a nuvem, considerando uma integração melhor com todos os recursos.

- **Exemplo:** Encerrar um contrato com fornecedor de CRM on premise para comprar um CRM adaptado para a nuvem no AWS Marketplace.

## Refactoring
- Considerado quando você precisa alterar e refatorar código da aplicação, adicionar novas features que só funcionam na nuvem, e não no on premise.

- **Exemplo:** utilizar o SDK da AWS para fazer um sistema que utiliza arquitetura de mensageria através do SQS.

## Retiring
- Remoção de recursos desnecessários para a aplicação, promovendo uma migração enxuta e sem falhas.

- **Exemplo:** Remoção de features ou componentes que não são mais úteis no funcionamento da aplicação.

## Retain
- Utilizar este conceito na migração de aplicações aposentadas, que ainda estão sendo utilizados somente para recuperar arquivos, fazer queries ou obter exemplos.

- Essa estratégia também deve ser consideradas em casos de aplicações que não podem ficar offline nem por um minuto. Nesse caso, devemos adiar a migração de maneira a aguardar o momento oportuno.

- Em casos como este, a AWS recomenda adiar a migração para o momento ideal.

- **Exemplo:** Mainframes e bancos de dados aposentados/legados