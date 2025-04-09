Estas são algumas anotações mais avançadas de EC2, originadas dos estudos para a certificação SysOps Administrator.


## Instâncias Burstable (t2/t3)
- ==Instâncias burst possuem a capacidade de aumentar a capacidade de sua CPU em momentos de pico de utilização==, este é o chamado "burst".

- Quando a máquina entra em processo de burst, ela começa a utilizar créditos de CPU.

- ==Se todo o crédito acabar, a CPU ficará com a capacidade bem ruim e lenta==.

- Quando a máquina para o processo de burst seus créditos voltam a subir.

- Os créditos sobem conforme a máquina se mantém em uma baseline padrão.

- Se a sua instância fica com baixos créditos frequentemente, talvez seja uma boa opção utilizar outra família de instância.

- É possível definir a sua instância como **ilimitada**, garantindo créditos de CPU ilimitados, dessa forma, você irá pagar mais caro caso você consuma muito dos seus créditos de instância.
## Shutdown Behavior
- É possível modificar o comportamento de desligamento da instância, isto é, escolher se quando você desligar a instãncia ela entrará em estado `stopped` ou se a terminação deverá ser feita (`terminated`).


## Instance Connect
- O Instance Connect é uma maneira de acessar sua instância EC2 via SSH.

- Para que você consiga se conectar com a instância via Instance Connect, você precisa liberar a faixa de IP da AWS correspondente à região da instância: veja a [lista de IPS](https://ip-ranges.amazonaws.com/ip-ranges.json). (Sim, o **IP da AWS** é quem acessa a instância).