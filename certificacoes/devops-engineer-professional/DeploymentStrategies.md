# Deployment Strategies
- Estratégias de implantação são abordagens para lançar novas versões de software, garantindo a continuidade do serviço e minimizando riscos, estes tópicos são essenciais para o exame DevOps Engineer Professional, pois envolvem práticas de entrega contínua e integração contínua (CI/CD).

- Vejamos abaixo as principais estratégias de implantação.

## Blue/Green Deployment
- Consiste em manter duas versões do ambiente de produção: a versão atual (Blue) e a nova versão (Green).

- O tráfego é direcionado para a versão Blue, enquanto a versão Green é atualizada e testada. Após a validação da nova versão, o tráfego é redirecionado para ela, tornando-a a nova versão de produção.

- Essa estratégia minimiza o tempo de inatividade e permite um rollback rápido para a versão anterior em caso de problemas.

## Canary Deployment
- Envolve lançar a nova versão para um pequeno subconjunto de usuários (o "canário") antes de disponibilizá-la para toda a base de usuários.

- Isso permite monitorar o desempenho e a estabilidade da nova versão em um ambiente de produção real, identificando e corrigindo problemas antes de um lançamento completo.

## Rolling Deployment
- A nova versão é implantada gradualmente em partes do ambiente de produção, substituindo a versão antiga em etapas.

- Por exemplo, em um ambiente com 10 servidores, a nova versão é implantada em 2 servidores de cada vez, até que todos os servidores estejam rodando a nova versão.

- Essa abordagem reduz o risco de falhas, pois apenas uma parte do ambiente é afetada a cada vez, permitindo um rollback mais fácil se necessário.

## Rolling with Additional Batch
- Similar ao Rolling Deployment, mas em vez de substituir os servidores antigos, **a nova versão é implantada em servidores adicionais, aumentando a capacidade total durante a implantação**.

- Após a implantação, o tráfego é gradualmente redirecionado para os novos servidores, e os servidores antigos são desativados ou removidos.

## In-place Deployment
- A nova versão é implantada diretamente sobre a versão antiga, sem manter ambas as versões simultaneamente.

- É uma abordagem mais rápida e que consome menos recursos, mas apresenta um risco maior de falhas, pois não há um ambiente paralelo para testes ou rollback rápido.

- Essa estratégia é adequada para mudanças menores ou quando o tempo de inatividade é aceitável.

## Linear Deployment
- A nova versão é implantada para um percentual fixo de usuários em intervalos regulares, por exemplo, 10% dos usuários a cada hora, aumentando de maneira **linear** até atingir 100%.

- Isso permite uma transição suave e monitoramento contínuo, reduzindo o risco de falhas em larga escala.