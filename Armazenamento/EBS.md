# EBS
- O Elastic Block Store oferece um sistema de armazenamento baseado em 
blocos, como em discos físicos, ao contrário do S3, que é baseado em objetos.

- Volumes do EBS são fixos a uma só AZ! Para replicar volumes entre AZs,
crie um snapshot para montar o volume em outra AZ.

Observação: Você pode desacoplar um EBS de uma instância enquanto ela 
está rodando (on the fly).

## Tipos de EBS
### General Purpose - SSD - gp
- SSD de uso geral, equilíbrio entre preço e performance, para dados 
diversos.
- **Use Case**: Uso geral
- **Nome da API**: gp2 / gp3
- <span style="background-color: #e0a800; color: black;font-weight:bold">Este é o modelo padrão para root volumes</span>

### Provisioned IOPS - SSD - io
- SSD de alta performance, criado para aplicações críticas.
- **Use Case**: Bases de dados
- **Nome da API**: io1 / io2

### Throughput Optimized - HDD - st
- HD de Baixo custo, utilizado para workloads mais intesos e armazenamento de dados que precisam ser acessados frequentemente.
- **Use Case**: Big data & Data Warehouse
- **Nome da API**: st1

### Cold - HDD - sc 
- Disco de baixíssimo custo, utilizado para armazenar dados acessados com menos frequência
- **Use Case**: Servidor de Arquivos
- **Nome da API**: sc1


### Magnetic
- Disco rígido da geração passada.
- **Use Case**: Cenários onde os arquivos e dados são acessados raramente.
- **Nome da API**: standard

**OS MODELOS <span style="color:red "><ins>s</ins>c e <ins>s</ins>t</span> NÃO PODEM SER USADOS COMO BOOT VOLUMES. 
#FicaADica: viu S, não comece.**

## Multi-Attach
- Este é o processo de atrelar um mesmo volume EBS a múltiplas instâncias EC2 (obrigatoriamente na mesma AZ)

- Cada instância tem permissão completa de leitura e escrita.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Use case ideal seria para atingir uma disponibilidade maior</span> em aplicações clusterizadas.

- <span style="background-color: #e0a800; color: black;font-weight:bold">Limitada a 16 instância por vez.</span>

- Somente volumes io1 e io2 permitem multi-attach (caríssimos)

## Snapshot
<span style="background-color: #e0a800; color: black;font-weight:bold"> Um snapshot é o salvamento do estado de um disco do EBS, bem útil para backups. A partir dele você também pode criar uma nova imagem de máquina, as AMIs,</span> que por sua vez, também podem ser criadas a partir de template do S3 **Instance Store**.

Para instâncias baseadas em **Instance Store** (armazenamento da 
instância), o AMI é criado a partir de um template armazenado no Amazon

### Snapshot Archive
- Move um snapshot para uma "camada de arquivamento" do S3, o que torna seu armazenamento 75% mais barato.
- <span style="background-color: #e0a800; color: black;font-weight:bold">LEVA DE 24 A 72 HORAS PARA RESTAURAR O ARQUIVO</span>.

### Recycle Bin
- É possível definir uma regra para reter snapshots após a deleção deles.
- O período de retenção deve ser especificado, pode ser de 1 dia até 1 ano.

## Instance Store
- O Instance Store é um armazenamento temporário que é perdido quando a instância é encerrada. 

- <span style="background-color: #e0a800; color: black;font-weight:bold">Os Instances Store estão acoplados físicamente junto à instância lá no data center da AWS</span>, portanto, o armazenamento não está ligado com a instância através da rede, <span style="background-color: #e0a800; color: black;font-weight:bold">o que garante altíssima velocidade</span>.

- AMIs criadas a partir de um Instance Store são geralmente usadas para casos em que o armazenamento persistente não é necessário.

## Criptografia
É possível realizar a criptografia de um volume EBS através de um snapshot, seja este snapshot criptografado ou não. Porém não é possível realizar a criptografia de um volume EBS "on the fly", de fato, será necessário primeiro gerar um snapshot dele e então criar uma cópia idêntica deste volume.