# Elastic Beanstalk

O BeanStalk é um serviço que permite a construção automática de um ambiente de infraestrutura baseada no código da aplicação, muito útil para desenvolvedores que não desejam se preocupar com a infraestrutura do projeto, apenas com o código em si.

Dependendo da sua aplicação, podem ser gerados recursos relacionados a:
- Capacidade
- Balanceamento de carga
- Escalonamento automático
- Monitoramento de disponibilidade da aplicação

O BeanStalk também permite salvar um ambiente, de maneira que você pode copiá-los ou recriá-los facilmente.

## Tipos de ambientes
Ao criar um ambiente no Elastic Beanstalk, você pode escolher entre dois tipos principais:
- **Web Server Environment**: Projetado para hospedar aplicações web que respondem a solicitações HTTP/HTTPS. Ele inclui um servidor web (como Apache, Nginx, etc.) e é ideal para aplicações que precisam ser acessadas via navegador.

- **Worker Environment**: Projetado para executar tarefas em segundo plano ou processar filas de trabalho. Ele é usado para aplicações que não precisam responder diretamente a solicitações web, mas sim realizar processamento assíncrono, como processamento de dados, envio de e-mails, etc.

## Deployment policies
**Deployment Policies** no **Elastic Beanstalk** são estratégias que definem **como as novas versões da sua aplicação são implementadas (deploy)** nas instâncias EC2. Cada política oferece níveis diferentes de **velocidade, disponibilidade e segurança**. Vejamos os tipos de deployment policies:

- **All at Once** - Faz o deploy de todos as instâncias de uma só vez, ao mesmo tempo em que apaga todas as instâncias originais, causando indisponibilidade. ==É basicamente um rolo compressor.==

- **Rolling** - Deploy feito em lotes, as instâncias são tiradas de cena uma de cada vez. ==Disponibilidade parcial é mantida==.

- **Rolling with additional batch** - ==Mesma estratégia do _Rolling_, porém provisionando algumas instâncias extras temporariamente==, visando manter a disponibilidade durante o deploy.

- **Immutable** - Cria um novo conjunto completo de instâncias separadamente. Quando tudo estive OK, troca o tráfego e depois remove as instâncias antigas. **==Esse aqui é o famoso Blue/Green==**.

#### 📊 Comparativo Rápido

| **Policy**                  | **Disponibilidade** | **Tempo do Deploy** | **Custo Temporário** | **Segurança / Facilidade de Rollback** |
| --------------------------- | ------------------- | ------------------- | -------------------- | -------------------------------------- |
| **All at Once**             | ❌ Indisponível      | ✅ Muito rápido      | ✅ Baixo              | ❌ Baixa                                |
| **Rolling**                 | 🟡 Parcial          | 🟡 Moderado         | ✅ Baixo              | 🟡 Moderada                            |
| **Rolling with Additional** | ✅ Alta              | 🟡 Moderado         | 🟡 Moderado          | ✅ Alta                                 |
| **Immutable**               | ✅ Alta              | ❌ Mais lento        | 🟡 Moderado          | ✅ Muito Alta                           |

## Suporte a Docker
- O Elastic Beanstalk suporta aplicações containerizadas usando Docker.
- Você pode implantar aplicações Docker de duas maneiras:
  - **Single Container**: Para aplicações simples que rodam em um único contêiner Docker.
  - **Multi-Container**: Usando o Docker Compose para definir e gerenciar múltiplos contêineres Docker em um ambiente Elastic Beanstalk.
- O Elastic Beanstalk gerencia automaticamente a infraestrutura subjacente, incluindo o provisionamento de instâncias EC2, balanceamento de carga e escalonamento automático para aplicações Docker.
- **O arquivo `Dockerrun.aws.json` é usado para configurar aplicações Docker no Elastic Beanstalk**, especificando detalhes como a imagem Docker, portas expostas e volumes.