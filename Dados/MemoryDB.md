# MemoryDB

- O MemoryDB é um serviço de banco de dados em memória totalmente gerencial, durável e compatível com Valkey e Redis, projetado para aplicativos modernos que exigem latência de microsegundos e alta taxa de transferência.

- Ele é ideal para casos onde se exige alta performance, baixa latência e durabilidade dos dados, como em sessões de jogos, caching de dados críticos, e análise em tempo real.

## MemoryDB x ElastiCache
- Ambos são serviços de banco de dados em memória oferecidos pela AWS, mas possuem diferenças significativas em termos de arquitetura, durabilidade e casos de uso.

- O ElastiCache é mais focado em caching simples e rápido, enquanto o MemoryDB é projetado para oferecer durabilidade e alta disponibilidade, com replicação automática e recuperação de falhas.

- O MemoryDB oferece persistência de dados, o que significa que os dados podem ser recuperados após falhas, enquanto o ElastiCache é mais volátil. **O MemoryDB possui inclusive suporte nativo para snapshots e backups automáticos.**