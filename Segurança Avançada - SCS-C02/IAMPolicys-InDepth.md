Para ir bem no exame, é muito importante enter a lógica das policies da AWS

![[PolicyStructure.png]]

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