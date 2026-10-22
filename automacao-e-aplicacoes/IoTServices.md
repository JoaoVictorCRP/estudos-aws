# Serviços de IoT da AWS

A AWS possui um leque bem extenso de serviços de IoT (Internet Of Things), muitos destes serviços são cobrados em exames como o Solutions Architect Associate e Professional. Vejamos os principais:

## IoT Core 🫀
> Serviço central para conectar, autenticar, autorizar e receber dados de milhões de dispositivos IoT, sem provisionar ou gerenciar servidores.

- Usa protocolos como **MQTT, HTTP e WebSockets**.

- **Device Shadow**: armazena e sincroniza os estados dos dispositivos, sendo um "estado desejado" e um "estado atual", ideal para dispositivos com conexão limitada à nuvem.

- **Rules Engine**: permite rotear mensagens para **Lambda, DynamoDB, Kinesis, SNS, S3, etc.**

- Suporta autenticação via **certificados X.509**, **IAM** e **Cognito**

#### Aparece na prova quando:
- A questão envolve **comunicação bidirecional** com dispositivos.
- Precisa de roteamento de dados de dispositivos para backends (ex: Lambda, DynamoDB).
- Exige **gerenciamento de estados offline (Device Shadow)**.

---
## IoT Greengrass 📍
> Permite executar **funções Lambda**, coletar dados, tomar decisões e comunicar com IoT Core **localmente**, **sem depender da nuvem o tempo todo**.

- Roda em dispositivos de borda (ex: gateways, Raspberry Pi) através de um runtime.

- **==Pode funcionar offline e sincronizar dados depois==**.

- Suporta **machine learning local**, **containers**, **StreamManager**, etc.

#### Aparece na prova quando:
- Há ==requisito de **baixa latência**, **operação offline**, ou processamento local==.
- Precisa evitar ida e volta constante com a nuvem.
---
## IoT Device Management 📲
> Ferramenta para **registrar, organizar, monitorar e atualizar remotamente um ==grande número de dispositivos==**.

- Permite agrupar dispositivos, aplicar **atualizações OTA**, visualizar logs e estados.

- Cria **fleet indexes** e faz **busca por atributos de dispositivos**.

- Intregado com IoT Core e IoT Greengrass.

#### Aparece na prova quando:
- Você precisa de **atualização em lote** ou **gerenciamento centralizado de dispositivos**.
- O cenário envolve **milhares de dispositivos com gerenciamento em escala**.
---
## IoT Analytics 🔎
> Análise **serverless** de dados gerados por dispositivos IoT.

- Prepara, filtra, transforma e armazena dados em pipelines.

- Pode integrar com **QuickSight** ou **ML com Jupyter Notebooks**

### Aparece na prova quando:
- A questão foca em **análise de dados IoT (tempo ou tendência)** sem montar cluster
- Você quer transformar dados antes de armazenar em um Data Lake.
---
## IoT Device Defender 🛡️
> Garante **segurança em tempo real** dos dispositivos IoT.

- Detecta anomalias, desvios de comportamento.

- Audita políticas, certificados e permissões.

- Pode **bloquear ou isolar** dispositivos automaticamente.

### Aparece na prova quando:
- Cenário **exige detecção de comportamento malicioso em dispositivos**.
- Há necessidade de auditar certificados e políticas