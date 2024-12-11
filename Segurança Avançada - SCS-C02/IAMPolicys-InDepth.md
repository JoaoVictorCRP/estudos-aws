Para ir bem no exame, é muito importante enter a lógica das policies da AWS

![[PolicyStructure.png]]

---
## NotAction 
O NotAction realiza a negação de um efeito, vejamos como funciona...

### NotAction with Allow
- Permite acesso a tudo os recursos listados em resouce, menos o que estiver incluso em **NotAction**.
```
	{
		"Version":"2012-10-17"
		"Statement": [
			{
				"Effect": "Allow"
				"NotAction": "iam:*"
				"Resource":"*"
			}
		]
	}
```
No exemplo acima, o usuário tem acesso a tudo, menos o IAM.

---
## Condition
- 🅰️ **StringEquals** / **StringNotEquals** - *Case sensitive*. Específica uma ==combinação exata== de caracteres.

```
"StringEquals": {
	"aws:PrincipalTag/job-category":["iamuser-admin"]
}
```


- 🅰️ **StringLike** - *Case sensitive*. Permite combinação parcial utilizando as wildcards "\*" ou "?"
```
"StringLike": {
	"s3:prefix":["", "home/*/data/", "home/${aws:username}/"]
}
```


- 📅 **DateEquals, DateLessThan, DateGreaterThan** - Permite comparação de data
```
"DateGreaterThan": {
	"aws:TokenIssueTime":["2020-01-01T00:00:01Z"]
}
```


- 🪪 **ArnLike/ArnNotLike** - Usado para verificações de ARN.
```
"ArnEquals": {
	"aws:SourceArn": "arn:aws:sns:sa-east-1:123456789011:TOPIC-ID"}}
}
```


- ✅ **Bool** - Validação booleana
```
"Bool": {
	"aws:SecureTransport":"false"
}
```


- 🌐**IpAddress / NotIpAddress** - Validação do endereço IP qual a requisição se originou (Só funciona para verificar IP público, portanto não dá pra usar isso para requisições dentro da sua própria VPC)
```
"IpAddress": {
	"aws:SourceIp":"203.0.113.0/24"
}
```

---
## Context Keys nas Conditions
Context Keys aparecem dentro de Conditions como parâmetros para realização das operações lógicas de validação. Vejamos:

#### RequestedRegion
- Essa é uma chave utilizada dentro de uma validação de string, onde podemos estabelecer a condição de que a política só é valida se a região do request veio da região, ou das regiões, especificadas.
 ![[RequestedRegion-1.png]]

##### CUIDADO COM A PEGADINHA!
Quando você estiver especificando uma política para um ==serviço global==, tipo o CloudFront, IAM, Route 53, dentre outros, ==a região sempre será **us-east-1**==
![[RequestedRegion-2.png]]
A policy acima está dizendo, basicamente, "Negue todos os recursos caso o request venha da Europa, exceto Cloudfront, IAM, Route 53 e Support"

#### Principal ARN
Realiza uma comparação do ARN da entidade que realizou o request com o ARN específicado na policy

**NOTA**: ==Caso usuário esteja por trás de uma role, o ARN analisado será o da Role==, e não do usuário que a utiliza.

#### Source ARN
Compara o ARN do recurso que está fazendo o request service-to-service com o ARN que foi especificado na policy.

 **NOTA**: ==Essa chave só é utilizada quando um recurso AWS está tendo acessar outro recurso AWS==, portanto não confunda com o Principal ARN, que é para caso de usuários.

#### IP & VPC
- **aws:SourceIp** => ==IP público== do solicitante.

- **aws:VpcSourceIp** => ==IP privado== do solicitando (dentro da sua VPC)

- **aws:SourceVpce** => Restringe o acesso para um ==VPC Endpoint== específico.

- **aws:SourceVpc** => Restringe o acesso para uma ==VPC específica==.

**NOTA**: estas regras são bastante utilizadas nas bucket policies do S3.