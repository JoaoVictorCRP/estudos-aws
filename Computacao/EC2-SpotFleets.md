# Spot Fleets
Spot fleets é um tema recorrente no exame do SSA-C03. Veja alguns detalhes deste modelo do Spot instances:

### Como Funciona o Spot Fleet?

1. **Definindo a Fleet:**
    - Quando você cria uma Spot Fleet, você especifica:
        - **Tipos de Instância:** A lista de tipos de instância que você está disposto a usar (por exemplo, `t3.micro`, `m5.large`).
        - **Zonas de Disponibilidade:** As zonas de disponibilidade onde a Spot Fleet pode iniciar instâncias.
        - **Peso das Instâncias:** Opcionalmente, você pode atribuir pesos diferentes a tipos de instâncias com base em suas capacidades (por exemplo, uma `m5.large` pode valer o dobro de uma `t3.micro`).
        - **Capacidade-Alvo:** A capacidade total que você deseja alcançar (pode ser definida em termos de instâncias ou capacidade computacional).
        - **Estratégia de Alocação:** A estratégia que a Spot Fleet deve usar para selecionar as instâncias, como a de menor preço ou a de diversificação (ver mais abaixo).
        
2. **Estratégias de Alocação:**
- **Lowest Price (Menor Preço):** A Spot Fleet tenta lançar as instâncias mais baratas disponíveis até atingir a capacidade desejada. Isso maximiza a economia, mas pode aumentar o risco de interrupção se os preços subirem.
- **Diversified (Diversificada):** A Spot Fleet distribui as instâncias entre diferentes tipos e zonas de disponibilidade. Isso reduz o risco de interrupções, já que é menos provável que todas as zonas e tipos sejam interrompidos ao mesmo tempo.
- **Capacity Optimized (Otimizada para Capacidade):** A Spot Fleet escolhe instâncias em grupos que têm a maior capacidade disponível, reduzindo o risco de interrupção ao evitar grupos de instâncias que estão quase esgotados.

1. **Gerenciamento Automático:**
    - A Spot Fleet monitora constantemente os preços das Spot Instances e a disponibilidade das instâncias. Se o preço de um tipo de instância subir acima de um nível aceitável ou se a instância for interrompida, a Spot Fleet automaticamente tenta substituir essa instância por outra que atenda aos critérios especificados.
    - A Spot Fleet também pode ajustar dinamicamente a capacidade com base na demanda ou nos parâmetros definidos, como políticas de Auto Scaling.
    
2. **Opções de Requisição:**
    - **Maintain (Manter):** A Spot Fleet tentará sempre manter o nível de capacidade desejado. Se uma instância for interrompida, ela será substituída automaticamente.
    - **Request (Solicitar):** A Spot Fleet simplesmente solicita as instâncias e as mantém enquanto o preço permite. Não há tentativa de substituição automática em caso de interrupção.
    - **Submit (Enviar):** A Spot Fleet cria uma única requisição de Spot Instances. Não há substituição automática ou ajustes dinâmicos.

**Porque usar isto?**

Essa estratégia nos permite fazer pedidos automáticos por Spot Instances a preços baixos, a aplicação pode tolerar interrupções e falhas, uma Spot Fleet pode ajudá-lo a economizar significativamente em comparação com o uso de instâncias sob demanda.