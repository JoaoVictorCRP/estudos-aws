Estas são algumas anotações mais avançadas de EC2, originadas dos estudos para a certificação SysOps Administrator.

## Shutdown Behaviour
- É possível modificar o comportamento de desligamento da instância, isto é, escolher se quando você desligar a instãncia ela entrará em estado `stopped` ou se a terminação deverá ser feita (`terminated`).


# Instance Connect
- O Instance Connect é uma maneira de acessar sua instância EC2 via SSH.

- Para que você consiga se conectar com a instância via Instance Connect, você precisa liberar a faixa de IP da AWS correspondente à região da instância: veja a [lista de IPS](https://ip-ranges.amazonaws.com/ip-ranges.json). (Sim, o **IP da AWS** é quem acessa a instância).