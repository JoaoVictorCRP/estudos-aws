# Fundamentos da Prova - Networking Specialty

- O CIDR máximo de uma VPC é /16 (65.536 IPs), e o mínimo é /28 (16 IPs).

- Em cada subnet, 5 IPs são reservados pelo AWS, sendo os 4 primeiros e o último IP do range da subnet.

- Para alta disponibilidade, recomenda-se criar um NAT Gateway em cada AZ.

- NAT Instances são mais baratas, mas não são escaláveis e não são gerenciadas pelo AWS.