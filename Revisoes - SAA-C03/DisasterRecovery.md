Questões específicas sobre estratégias de disaster recovery (DR) são bem comuns no exame SAA-C03. Vejamos... 

## Termos Chaves

### **RPO**
- Significa Recovery Point Objective

- "De quanto em quanto tempo eu realizo backups?"

- "Se necessário, eu consigo voltar a qual ponto no tempo com a minha infraestrutura?"
 
- Suponhamos que ocorreu, às 13h um desastre ambiental inesperado que destruiu o seu data center. Nesse caso, se você realiza backups toda madrugada, às 3h da manhã, você perdeu 10h de dados.

### **RTO**
- Significa Recovery Time Objective	

- Se um desastre ocorrer, em quanto tempo eu consigo me recuperar?"	

- Utilizando aquele exemplo acima, o desastre ambiental ocorreu às 13h e eu irei conseguir restaurar o backup às 14h, ou seja, 1h de downtime. Portanto, 1h de RPO.

![[RPO-RTO.png]]

## Estratégias de DR

### Backup and Restore
- ==**O RPO é alto.**==
- Caracteriza-se pela criação de backups de tempos em tempos.

- ==**RTO moderado/alto**==, pois quanto maior a quantidade de dados, mais tempo o backup levará para ser restaurado, na maioria dos casos levará bem mais que 1h.

- Apesar de tudo, ==é uma estratégia bem barata==, o único custo que se tem é o de armazenamento dos backups.
#### Exemplos
- Data centers que enviam dados para a AWS semanalmente com Snowball. Se o Datacenter pegar fogo, ou algo do tipo, uma semana inteira de dados pode ser perdida

- Snapshots de um EBS, RDS ou Redshift que são criados regularmente (quanto menor o intervalo de realização do snapshot, menor o RPO).

### Pilot Light
- Baseia-se em deixar a parte crítica de um sistema sempre rodando, que possui replicação contínua com a versão principal.

- Utilizado para proteger a parte crítica do sistema, que precisa sempre estar rodando, dessa forma, se o hospedeiro on-premise de uma aplicação falhar, por exemplo, é só ajustar o DNS para apontar para o servidor na nuvem.

- Mais rápido que o Backup and Restore, porém um pouco mais caro.

- ==**RPO moderado**, **RTO moderado**==

- Opção bem ==popular com sistemas que possuem um núcleo crítico==.

- Fazendo uma analogia, ==imagine essa estratégia como se fosse uma luz de emergência quando a energia acaba.==

### Warm Standby
- Uma ==cópia== do sistema que utiliza ==recursos mínimos== está =="no banco de reserva".==

- ==Quando o desastre ocorrer, os recursos da cópia recebem um upgrade==, para que eles possam aguentar a carga de produção.

- ==**RPO baixo, RTO baixo (ou moderado)**==

### Hot site / Multi Site
- Caracteriza-se por deixar uma ==cópia completa do sistema, com recursos exatos aos de produção.==

- Em muitos casos, já se utiliza um weighted route no route 53 para rotear para ambos os ambientes, se um deles cai, o outro toma a frente.

- **Muuito caro**

- ==**RTO e RPO Baixíssimos**==