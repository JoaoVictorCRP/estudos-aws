# EC2

## User Data

É possível incluir um script que rodará na primeira vez que a instância for iniciada, chamado user data, neste script é possível automatizar tarefas como:

- Instalação de atualizações
- Instalação de softwares
- Baixar arquivos da internet
- E muitas outras coisas…

O script de User Data roda na conta do usuário root, por tanto todos os comandos dados tem o privilégios sudo.

![Tipos](images/ec2-tipos.png)

## Detalhes das Instâncias

### O Nome

![Nomes](images/ec2-nomes.png)

### **Os Tipos**

- **General Purpose**:
    - Equilíbrio entre processamento, memória e rede.
    - Estarei utilizando o t2.micro, que é uma instância do tipo *General Purpose*.
    - **Use case**: Sites e aplicativos web, ambientes de desenvolvimento, servidores de compilação repositórios de código, microsserviços, ambientes de teste e preparação e aplicativos de linha de negócios.

![GP](images/ec2-GeneralPurpose.png)

- **Compute Optimized**:
    - Instância que possui foco no poder de processamento (CPU).
    - **Use case**: Computação de alta performance (HPC), processamento em lote, veiculação de anúncios, codificação de vídeo, jogos, modelagem científica, análise distribuída e inferência de machine learning com base em CPU.
    
    ![CO](images/ec2-ComputeOptimize.png)
    

- **Memory Optimized**:
    - São projetadas para fornecer performance rápida para workloads que processam grandes conjuntos de dados na memória.
    - **Use case**: Workloads que consomem muita memória, como bancos de dados de código aberto, caches na memória e análise de big data em tempo real.
    
    ![MO](images/ec2-MemoryOptimized.png)
    

- **Storage Optimized**:
    - Ótimas para tarefas que exigem alta capacidade de armazenamento, isto é, acesso a leitura e escrita de uma grande quantidade de dados no disco local.
    - **Use case**: Aplicações intensivas de E/S, são instâncias direcionadas a clientes que usam bancos de dados transacionais (Amazon DynamoDB, MySQL e PostgreSQL), Amazon OpenSearch Service, Aplicações de Data warehouse e análises em tempo real, como o Apache Spark.
    
    ![image.png](images/ec2-StorageOptimized.png)
    

## **Grupos de Segurança**

- Os **Security Groups** são o ponto chave da segurança de rede na AWS.
- Eles controlam como o tráfego de E/S é permitido ou negado para a EC2.
- Security Groups possuem somente regras de allow
- As regras dos **Security Groups** podem referenciar por IP ou por outro Security Group **(SGs podem referenciar uns aos outros).**

No esquema de referência a outro grupo de segurança, indica que o tráfego está liberado para qualquer instância que faça parte daquele grupo referenciado, independente do IP, bom demais.

![image.png](images/ec2-SecurityGroups.png)

Basicamente, Grupos de Segurança agem como firewalls para instâncias EC2.

Eles regulam:

- Acesso a portas;
- Faixas de IP liberadas (IPv4 e IPv6);
- Controle de conexões **inbound** (de um dispositivo externo para a instância);
- Controle de conexões **outbound** (Da instância para dispositivo externo);

![image.png](images/ec2-SecurityGroups2.png)

## Opções de Cobrança

![Cobranca](images/ec2-cobranca.png)

![Exemplo](images/ec2-cobrancaExemplo.png)

![Precos](images/ec2-cobrancaPrecos.png)

## Interfaces de Rede

### **ENI (Elastic Network Interface) - Padrão:**

- **Definição:** Uma ENI é uma interface de rede virtual que pode ser anexada a uma instância EC2. Ela funciona como uma interface de rede física, contendo um endereço IP primário, um ou mais endereços IP secundários, um ou mais grupos de segurança, um endereço MAC, e outras configurações de rede.
- **Uso:** ENIs são usadas para conectar instâncias EC2 a sub-redes em uma VPC. Elas permitem que você mova interfaces entre instâncias, o que pode ser útil para cenários de alta disponibilidade ou para isolar diferentes tipos de tráfego.
- **Exemplo de Aplicação:** Ter múltiplas interfaces de rede em uma instância para segmentar o tráfego de rede ou para separar diferentes camadas de aplicação.

### **ENA (Elastic Network Adapter) - Alta Performance:**

- **Definição:** O ENA é um adaptador de rede de alta performance projetado para oferecer suporte a Enhanced Networking na AWS. Ele oferece maior largura de banda, menor latência, e menor sobrecarga em comparação com as interfaces de rede padrão.
- **Uso:** ENA é usado principalmente em instâncias EC2 que exigem alta performance de rede, como em aplicações de HPC (High-Performance Computing) e grandes clusters de dados.
- **Exemplo de Aplicação:** Quando uma instância EC2 precisa de uma largura de banda de rede de até 100 Gbps, como em simulações científicas ou análises de Big Data.

### **EFA (Elastic Fabric Adapter) - Potência Máxima:**

- **Definição:** O EFA é um adaptador de rede que fornece latência ultrabaixa e alta taxa de transferência, além de suporte para aplicativos de HPC que usam bibliotecas de comunicação de rede como MPI (Message Passing Interface). **O EFA não é compatível com as instâncias do Windows.**
- **Uso:** EFA é especificamente projetado para workloads HPC que requerem uma comunicação de rede extremamente rápida e eficiente, como em simulações científicas, modelagem financeira ou análises de petróleo e gás.
- **Exemplo de Aplicação:** Aplicações HPC distribuídas que exigem uma comunicação rápida entre instâncias EC2 em um cluster, como no processamento de fluido dinâmico computacional (CFD) ou em renderização gráfica em 3D.

## Web Application Firewall (WAF)

Com este serviço, é possível monitorar as requisições HTTP/HTTPS que chegam em seus servidores, também é possível controlar quem acessa os seus conteúdos. É possível fazer diversas condições de bloqueio para requisições, por exemplo:

- Endereço de IP da origem
- País de onde a requisição se originou
- Valores na header
- Strings que aparecem no request body (regex)
- Tamanho da requisição
- Presença de código SQL (famoso SQL Injection)
- Presença de script malicioso (Cross-site scripting

## Placement Groups

São um recurso do Amazon EC2 que permite controlar o posicionamento de instâncias em hardware subjacente dentro de uma Availability Zone da AWS. Eles são usados para melhorar o desempenho da rede ou a resiliência das instâncias.

### Tipos de Placement Groups:

1. **Cluster**:
    - **Objetivo:** Maximizar o desempenho da rede ao agrupar instâncias próximas umas das outras no mesmo rack ou em racks adjacentes.
    - **Uso Ideal:** Workloads que exigem baixa latência e alta taxa de transferência entre instâncias, como HPC (computação de alto desempenho) e grandes bancos de dados distribuídos.
    - **Limitação:** Alta disponibilidade pode ser comprometida, pois as instâncias estão fisicamente próximas e podem ser afetadas por falhas no rack.
2. **Spread:** 
    - **Objetivo:** Garantir que as instâncias sejam distribuídas por diferentes racks, reduzindo o risco de falhas correlacionadas.
    - **Uso Ideal:** Aplicações críticas que precisam de alta disponibilidade e resiliência, onde as instâncias precisam estar em racks diferentes.
    - **Limitação:** Número máximo de instâncias por grupo espalhado é limitado (normalmente até 7 instâncias por grupo em algumas regiões).
3. **Partition**:
    - **Objetivo:** Distribuir instâncias em partições lógicas, onde cada partição tem seus próprios racks. Isso fornece isolamento entre grupos de instâncias dentro de uma partição. Partições podem estar em múltiplas AZ.
    - **Uso Ideal:** Grandes sistemas distribuídos, como Hadoop, HDFS, e Cassandra, onde a falha de uma partição não deve afetar as outras.
    - **Limitação:** Menor densidade de instâncias por partição comparado ao Cluster Placement Group.
    - A diferença entre Partition e Spread é que uma partição que fica em um rack pode incluir várias instancias, veja a imagem de exemplo onde temos 3 partições, cada uma em sua própria rack, e em cada partição temos 3 instâncias:

![image.png](/Computacao/images/ec2-partition.png)

### Cenários de Uso:

- **Cluster Placement Group:** Quando você precisa de baixa latência de rede, como em simulações científicas, machine learning, ou grandes bancos de dados.
- **Spread Placement Group:** Quando a prioridade é a resiliência, como em sistemas críticos que não podem ter todas as instâncias afetadas por uma única falha de hardware.
- **Partition Placement Group:** Para grandes sistemas distribuídos que requerem isolamento de falhas entre diferentes grupos de dados ou componentes do sistema.

### Resumo:

- **Cluster Placement Groups** são usados para otimizar o desempenho da rede.
- **Spread Placement Groups** garantem a alta disponibilidade distribuindo instâncias em racks diferentes.
- **Partition Placement Groups** oferecem uma abordagem híbrida que isola falhas entre partições.

## EC2 Hibernate
- O modo hibernate <span style="background-color: #e0a800; color: black;font-weight:bold">permite que você deixe a instância em uma espécie de "modo descanso", fazendo com que o estado da memória RAM seja preservado no EBS correspondente da instância.</span> É bem interessante quando se trata de poupar gastos sem perder o estado da máquina. Veja alguns detalhes:
    - <span style="color:red; font-weight: bold">A RAM da máquina deve ter:</span> 
        - **Menos de 150GB em SOs Linux**
        - **Menos de 16GB em SOs Windows**
    - <span style="background-color: #e0a800; color: black;font-weight:bold"> O volume root deve estar no EBS, ser criptografado,</span> **NADA DE INSTANCE STORE.** <span style="background-color: #e0a800; color: black;font-weight:bold">O EBS deve possuir tamanho proporcional à memoria RAM.</span>
    
    - Disponível em todos os tipos de aquisição de instância (**On-Demand, Reserved e Spot**)

    - Uma instância não pode hibernar por mais de 60 dias.


## Outros Detalhes

- Um único SG pode estar atrelado a múltiplas instâncias
- SGs são bloqueados a uma combinação região / VPC
- O usuário da EC2 não visualiza as regras de tráfico aplicadas a máquina dele
- É uma boa prática manter um SG exclusivo para acesso SSH.
- **Troubleshooting**:
    - Se a sua aplicação não está acessível (timeout), é problema no SG.
    - Agora, se a aplicação devolve um erro “conection refused”, então é um erro da aplicação, ou então ela não está aberta mesmo, pois o trafégo está ok.
- Por padrão:
    - **Todo tráfico inbound é bloqueado.**
    - **Todo tráfico outbound está autorizado.**


- Porta para lembrar: 

    - 3389 ⇒ RDP (Remote Desktop Protocol) - Logar em uma instância Windows.

- Elastic IP é o nome dado a opção de IP estático para as instâncias EC2.

- Por padrão, Scripts do User Data rodam com privilégio de root.