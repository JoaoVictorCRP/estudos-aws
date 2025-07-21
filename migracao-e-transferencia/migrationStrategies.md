# 7 R's
Para um processo de migração bem sucedido, a AWS lista 7 estratégias diferentes para o cumprimento deste objetivos, são os chamados 7 R's:

## **R**elocate
> Migrar ==**várias VMs ou clusters inteiros**== de um datacenter **para um ambiente gerenciado**, como o **VMware Cloud on AWS**, **sem alterar código ou arquitetura**.

- Foco: **mover o ambiente inteiro como está**, sem converter para EC2.
    
- **Exemplo**: migrar um cluster vSphere (com VMs Windows e Linux) para **VMware Cloud on AWS**.

## **R**ehosting (Lift and Shift)
> Envolve migrar a aplicação de um ambiente on-premises ou datacenter para **instâncias EC2 na AWS**, **sem nenhuma alteração no código**.

- **Foco**: mover de VM para VM.

- **Exemplo**: mover um servidor Linux com Apache e banco local para uma EC2 com a mesma configuração.

## **R**eplatforming (Lift and Reshape)
> Realizar otimizações para o funcionamento na nuvem, porém não mudar o core da arquitetura.
- **Foco:** Mover para cloud com pequenas otimizações.

- **Exemplo:** Migrar app para EC2, mas trocar o banco de MySQL local por RDS

## **R**epurchasing (Drop and Shop)
> Trocar por uma solução diferente hospedada na nuvem.

- **Foco**: Substituir por solução SaaS

- **Exemplo:** Encerrar um contrato com fornecedor de CRM on-premises para comprar um CRM adaptado para a nuvem no AWS Marketplace.

## **R**efactoring
> Reimaginar a arquitetura da aplicação com ferramentas e serviços da nuvem.

- **Foco**: Refatorar para arquitetura nativa em nuvem

- **Exemplo:** Trocar a arquitetura monolítica da sua aplicação on-premises para um modelo de micro serviços.

## **R**etire
> **Remover e aposentar aplicações e componentes desnecessários**, promovendo uma migração enxuta e sem falhas.

- **Foco:** Remover componentes e aplicações redundantes ou obsoletos.

- **Exemplo:** App legado sem uso real que pode ser desativado.

## **R**etain
> Manter a hospedagem atual como está, adiando a migração ou deixando ela de lado

- **Foco**: Manter como está

- Estratégia utilizada em casos de aplicações com questões não resolvidas de compliance, performance ou segurança.

- **Exemplo:** Sistema que só roda em máquina específica ou depende de hardware local

--- 
### Tabela Comparativa

| **Estratégia** | **O que é**                                | **Alterações no código?** | **Quando usar**                                                  | **Exemplo prático**                                                            |
| -------------- | ------------------------------------------ | ------------------------- | ---------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| **Rehost**     | "Lift and Shift" – mover para EC2          | ❌ Não                     | Migração rápida, sem alterar aplicação                           | Migrar app legado de servidor físico para EC2 com MGN                          |
| **Relocate**   | Mover VMs em massa sem conversão para EC2  | ❌ Não                     | Migração de ambientes VMware (vSphere)                           | Mover dezenas de VMs do vCenter on-prem para VMware Cloud on AWS               |
| **Repurchase** | Substituir por solução SaaS                | ✅ Sim (total)             | Quando é mais vantajoso pagar por uso do que manter app atual    | Trocar SAP on-prem por SAP S/4HANA Cloud, ou Exchange Server por Microsoft 365 |
| **Replatform** | Mover para cloud com pequenas otimizações  | ⚠️ Leves ajustes          | Quando há tempo para ajustes leves e ganho de eficiência         | Migrar app para EC2, mas trocar o banco de MySQL local por RDS                 |
| **Refactor**   | Refatorar para arquitetura nativa em nuvem | ✅ Sim (parcial ou total)  | Para tirar proveito total da escalabilidade e resiliência da AWS | Quebrar monólito em microsserviços usando Lambda, SQS e DynamoDB               |
| **Retain**     | Manter como está                           | ❌ Não                     | App ainda é necessário mas não será migrado agora                | Sistema que só roda em máquina específica ou depende de hardware local         |
| **Retire**     | Desligar o sistema                         | ❌ Não                     | App redundante ou obsoleto                                       | App legado sem uso real que pode ser desativado                                |