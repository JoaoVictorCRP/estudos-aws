# Questões Sobre Arquitetura de Custo Otimizado
Neste arquivo estão questões que eu errei sobre o design de arquiteturas com custo otimizado

___

## <span style="color:blue; background-color:#fff">CloudFront</span>
_**"A company offers an online product brochure that is delivered from a static website running on Amazon S3. The company’s customers are mainly in the United States, Canada, and Europe. The company is looking to cost-effectively reduce the latency for users in these regions. What is the most cost-effective solution to these requirements?"**_

- [X] <span style="background-color:red; color:#fff"> Create an Amazon CloudFront distribution that uses origins in U.S, Canada and Europe.
</span>

- [ ] Create an Amazon CloudFront distribution and use Lambda@Edge to run the website's data processing closer to the users.

- [ ] <span style="background-color:green; color:#fff">Create an Amazon CloudFront distribution and set the price class to use only U.S, Canada and Europe.
</span>

- [ ] Create an Amazon CloudFront distribution and set the price class to use all Edge Locations for best performance.

### **Explicação**
A origem pode ser em um lugar só, não há necessidade alguma de definir uma origem em diferentes regiões. A price class deve ser usada para determinar em qual lugar do mundo o cache de conteúdo ocorrerá, uma das opções é "US, Canada e Europa" que é justamente o que queremos aqui.

___
