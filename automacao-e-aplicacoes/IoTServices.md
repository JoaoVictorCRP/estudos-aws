A AWS possui um leque bem extenso de serviços de IoT (Internet Of Things), muitos destes serviços são cobrados em exames como o Solutions Architect Associate e Professional. Vejamos os principais:

## IoT Core
- Serviço central para conectar, autenticar, autorizar e receber dados de milhões de dispositivos IoT, sem provisionar ou gerenciar servidores.

- Usa protocolos como **MQTT, HTTP e WebSockets**.

- **Device Shadow**: armazena e sincroniza os estados dos dispositivos, sendo um "estado desejado" e um "estado atual", ideal para dispositivos com conexão limitada à nuvem.

- **Rules Engine**: permite rotear mensagens para **Lambda, DynamoDB, Kinesis, SNS, S3, etc.**

- Suporta autenticação via **certificados X.509**, **IAM** e **Cognito**

#### Aparece na prova quando:
- A questão envolve **comunicação bidirecional** com dispositivos.
- Precisa de roteamento de dados de dispositivos para backends (ex: Lambda, DynamoDB).
- Exige **gerenciamento de estados offline (Device Shadow)**.

---
## IoT Greengrass
- Permite executar **funções Lambda**, coletar dados, tomar decisões e comunicar com IoT Core **localmente**, **sem depender da nuvem o tempo todo**.

- Roda em dispositivos de borda (ex: gateways, Raspberry Pi).

- Pode funcionar offline e sincronizar dados depois.

- Suporta **machine learning local**, **containers**, **StreamManager**, etc.

#### Aparece na prova quando:
- Há requisito de **baixa latência**, **operação offline**, ou processamento local.
- Precisa evitar ida e volta constante com a nuvem.