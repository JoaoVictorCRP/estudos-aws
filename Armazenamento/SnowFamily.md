A **AWS SnowFamily** é um serviço que disponibiliza **dispositivos físicos** para facilitar a **migração massiva de dados** para a nuvem. Esses dispositivos são enviados para o endereço do cliente, onde os dados são carregados localmente. Após o carregamento, o dispositivo é devolvido para a **AWS**, que realiza o upload dos dados para a nuvem do contratante.

> Ideal para cenários em que o cliente tem muitos dados on-premises e uma conexão de internet limitada.

___
### **Dispositivos Disponíveis**:

- **Snowcone**: Capacidade de até **14TB**.
- **Snowball Edge**: Capacidade de até **120TB** (por dispositivo).

O cliente escolhe quantos dispositivos **Snowcones** ou **Snowball Edges** são necessários para a migração, dependendo do volume de dados.

|                        | **Snowcone** | **Snowball Edge** |
| ---------------------- | ------------ | ----------------- |
| **Capacidade**         | 8TB - 14TB   | 80TB - 210TB      |
| **Escala da Migração** | Terabytes    | Petabytes         |
___
### **Versões do Snowball Edge**:

O **Snowball Edge** oferece duas versões principais, ambas projetadas para permitir o **processamento de dados enquanto o dispositivo ainda está em trânsito**. ==Isso significa que você pode realizar processamento diretamente no Snowball Edge, sem esperar que ele chegue à AWS.==

- **Snowball Edge Compute Optimized (CO)**:
    - Ideal para cargas de trabalho que exigem mais capacidade de processamento, como análise de vídeo ou aplicações de machine learning.

- **Snowball Edge Storage Optimized (SO)**:
    - Projetado para migrações de grandes volumes de dados e cargas de trabalho que requerem maior capacidade de armazenamento, sem tanta necessidade de processamento.