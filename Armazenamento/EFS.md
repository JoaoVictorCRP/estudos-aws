# Elastic File System
- Sistema NFS (Network File System) gerenciado pela Amazon que pode ser montado em qualquer EC2.

- Funciona em instâncias EC2 com multi-AZ.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Alta disponibilidade, escalável e caro (3x o preço de um EBS gp2).
</span>

- Pay per use.

- **Use cases:** Gerenciamento de conteúdo, servidores web, compartilhamento de arquivos e Wordpress.

- Utilize security groups para controlar o acesso ao EFS.

## Performance

### Modos de taxas de transferência
- **Bursting**: Fornece throughput escalável de acordo com a quantidade de armazenamento para workloads com requisitos básicos de performance.

- **Enhanced**: Fornece mais flexibilidade e níveis de throughput mais altos para workloads com requisitos de performance diversos.

#### Configuração adicional para taxa de transferência
Após escolher uma das duas opções acima, é possível definir algumas opções avançadas para a performance:
- **Elastic**: Aumenta ou diminui automaticamente com base nas cargas de trabalho. Ideal para casos gerais.

- **Provisioned**: <span style="background-color: #e0a800; color: black;font-weight:bold">Se você puder estimar os requisistos de throughput das cargas de trabalho, use este modo.</span> Com ele, você configura a throughput e paga pelo provisionamento dela.

## Opções de Armazenamento
- **Padrão**: Essa é a opção de armazenamento padrão adequada para a maioria das cargas de trabalho, oferecendo um equilíbrio entre desempenho e custo.

- **One Zone**: Esta opção oferece armazenamento em uma única Zona de Disponibilidade, sendo mais econômica e útil para desenvolvimento ou backup. <span style="background-color: #e0a800; color: black;font-weight:bold">Também inclui a opção One Zone-IA, que é cerca de 47% mais barata que o armazenamento padrão e oferece economia de custos</span>.

Também é possível definir uma política de _lifecycle_ de arquivos, assim como no S3.

## Compatibilidade
- <span style="background-color: #e0a800; color: black;font-weight:bold">Só é compatível com AMI baseadas em Linux.</span>

## Segurança
- Criptografia me repouso com KMS.

## Anotações
- Como já foi dito, não é possível utilizar o EFS em sistemas Windows, no entanto, é possível utilizar um outro serviço com o mesmo intuito, o FSx em máquinas windows.