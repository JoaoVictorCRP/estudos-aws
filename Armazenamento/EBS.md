# EBS
- O Elastic Block Store oferece um sistema de armazenamento baseado em 
blocos, como em discos físicos, ao contrário do S3, que é baseado em objetos.

- Volumes do EBS são fixos a uma só AZ! Para replicar volumes entre AZs,
crie um snapshot para montar o volume em outra AZ.

Observação: Você pode desacoplar um EBS de uma instância enquanto ela 
está rodando (on the fly).

## Tipos de EBS
### General Purpose SSD
- SSD de uso geral, equilíbrio entre preço e performance, para dados 
diversos.
- **Use Case**: Uso geral
- **Nome da API**: gp2

### Provisioned IOPS SSD
- SSD de alta performance, criado para aplicações críticas.
- **Use Case**: Bases de dados
- **Nome da API**: io1

### Throughput Optimized HDD
- Disco rígido de baixo custo, utilizado para workloads mais intesos e 
armazenamento de dados que precisam ser acessados frequentemente.
- **Use Case**: Big data & Data Warehouse
- **Nome da API**: st1

### Cold HDD
- Disco rígido de baixo custo, utilizado para armazenar dados acessados 
com menos frequência
- **Use Case**: Servidor de Arquivos
- **Nome da API**: sc1

### Magnetic
- Disco rígido da geração passada.
- **Use Case**: Cenários onde os arquivos e dados são acessados 
infrequentemente.
- **Nome da API**: standard

## Snapshot
<span style="background-color: #e0a800; color: black;font-weight:bold"> Um snapshot é o salvamento do estado de um disco do EBS, bem útil para backups. A partir dele você também pode criar uma nova imagem de máquina, as AMIs,</span> que por sua vez, também podem ser criadas a partir de template do S3 **Instance Store**.

Para instâncias baseadas em **Instance Store** (armazenamento da 
instância), o AMI é criado a partir de um template armazenado no Amazon 

### Snapshot Archive
- Move um snapshot para uma "camada de arquivamento" do S3, o que torna seu armazenamento 75% mais barato.
- LEVA DE 24 A 72 HORAS PARA RESTAURAR O ARQUIVO.

### Recycle Bin
- É possível definir uma regra para reter snapshots após a deleção deles.
- O período de retenção deve ser especificado, pode ser de 1 dia até 1 ano.

## Instance Store
- O Instance Store é um armazenamento temporário que é perdido quando a instância é encerrada. 

- Os Instances Store estão acoplados físicamente junto à sua instância lá no data center da AWS, portanto, o armazenamento não está ligado com a instância através da rede, o que garante maior velocidade.

- AMIs criadas a partir de um Instance Store são geralmente usadas para casos em que o armazenamento persistente não é necessário.