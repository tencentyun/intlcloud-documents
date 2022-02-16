## Modo de faturamento
O TencentDB for TcaplusDB é compatível com os dois modos de faturamento abaixo:

| Tipo de instância | Modo de faturamento | Caso de uso |
|----|----|----|
|Edição cluster padrão|Pagamento conforme o uso|Esse modo de faturamento é adequado para ambientes de teste, de auditoria e de desenvolvimento. Você será cobrado de acordo com o pico de tráfego diário. Se nenhuma solicitação for feita para acessar o banco de dados, você só paga as taxas dos recursos mínimos reservados.|
|Edição de cluster autoimplantado|Pagamento conforme o uso|Esse modo de faturamento é adequado para o ambiente de produção. Você será cobrado diariamente de acordo com a quantidade de camadas de acesso e camadas de armazenamento. Você pode reduzir custos com o escalonamento automático. Por exemplo, você pode expandir a capacidade do cluster antes das campanhas com base nos picos de negócios estimados e reduzir a capacidade do cluster após as campanhas.|

## Ciclo de liquidação
As taxas incorridas no dia atual são faturadas no dia seguinte.

## Regras de faturamento para a edição de cluster padrão

A edição de cluster padrão adota o modo de faturamento com pagamento conforme o uso. As taxas diárias são calculadas com base nos picos de solicitações de leitura/gravação do banco de dados e no pico de capacidade do disco usado em um dia.

**Taxas diárias = Taxas de pico de capacidade de disco usado em um dia + Taxas de pico de unidades de capacidade de leitura (RCUs) em um dia + Taxas de pico de unidades de capacidade de gravação (WCUs) em um dia**

**Conceitos**
- **Capacity (Capacidade)**: os nomes da coluna de chave principal e da coluna de atributos são contabilizados no tamanho de cada linha de dados.
- **Read CU (Unidade de capacidade de leitura)**: uma operação de leitura de linha única de 4 KB por segundo é contabilizada como uma [unidade de capacidade de leitura (RCU)] reservada(https://intl.cloud.tencent.com/document/product/1016/36557).
- **Write CU (Unidade de capacidade de gravação)**: uma operação de gravação de linha única de 4 KB por segundo é contabilizada como uma [unidade de capacidade de gravação (WCU)] reservada(https://intl.cloud.tencent.com/document/product/1016/36557).
- **CU calculation rule (Regra de cálculo da unidade de capacidade)**: uma unidade capacidade (CU) é contabilizada separadamente no final de cada processo de solicitação e resposta. A CUs são acumuladas e calculadas com base na solicitação ou resposta (o que for maior). Dados menores que 4 KB são arredondados para os 4 KB mais próximos, e dados maiores que 4 KB são calculados em múltiplos de 4 KB. Por exemplo, se uma resposta de 9 KB for retornada para uma solicitação de 1 KB em um segundo, porque o tamanho da resposta é maior do que o da solicitação, a quantidade de CUs será calculada com base no valor da resposta. 9 KB é cerca de dois conjuntos de 4 KB, e o 1 KB restante é contabilizado como 4 KB, então a quantidade total de CUs será 2 + 1 = 3.
- **CU statistics rule (Regra de estatísticas de CU)**: as taxas diárias são calculadas com base no pico de acesso diário ao banco de dados. Se as leituras do banco de dados atingirem o valor mais alto às 12h de um dia, as RCUs desse momento serão usadas para calcular as taxas desse dia. Da mesma forma, se as gravações do banco de dados atingirem o valor mais alto às 15h01 de um dia, as WCUs nesse momento serão usadas para calcular as taxas desse dia.

### Preços

| Região | Capacidade (USD/GB/dia) | RCU (USD/CU/dia) |  WCU (USD/CU/dia)  |
|---------|---------|---------|---------|
| China Continental | 0,0052 | 0,0019 |  0,0048 |
|   Vale do Silício (Oeste dos Estados Unidos)  |0,006289|0,002| 0,0055 |
|Virgínia (Leste dos Estados Unidos)|0,006289|0,002|0,0055|
|Frankfurt (Alemanha)| 0,006 | 0,0022 | 0,0057 |
|  Singapura | 0,0061 |0,0025 | 0,0061 |
|   Hong Kong (China)  | 0,0055 |0,0019 | 0,0055 |
|   Japão  | 0,0055 |0,0019 |0,0055 |
|  Seul  |0,006289|0,002546|0,00599|

>?
> - As taxas são cobradas assim que um cluster é criado. O consumo mínimo diário de um cluster é de 1 GB de capacidade de disco, 80 RCUs e 26 WCUs. Mesmo se nenhuma tabela for criada, as taxas serão cobradas.
>  - Pelo menos 1 GB da capacidade do disco é reservado para um cluster padrão.
>  -  Pelo menos 80 RCUs são reservadas para um cluster padrão.
>  -  Pelo menos 26 WCUs são reservadas para um cluster padrão.
>-  A edição de cluster padrão aceita até 100 mil QPS. As solicitações além desse intervalo serão limitadas. Se sua empresa precisar de mais de 100 mil QPS, recomendamos que você use a edição de cluster autoimplantado, que fornece um desempenho maior e mais estável.
### Amostra de faturamento
Suponha que você crie um cluster na região de Xangai. Em um dia, o pico de solicitações de leitura é de 80 por segundo, o pico de solicitações de gravação é de 26 por segundo e o pico de capacidade do disco usado é de 0,5 GB.
As taxas diárias são calculadas da seguinte forma:

| Capacidade (GB) | Solicitações de leitura (RCU) |  Solicitações de gravação (WCU)  | Taxas |
|---------|---------|---------|-------|
| 1 | 80 |  26 | 1 GB × 0,0052 USD/GB/dia + 80 RCUs × 0,0019 USD/RCU/dia + 26 WCUs × 0,0048 USD/WCU/dia = 0,282 USD/dia|

Suponha que, com a promoção da empresa, os aplicativos interajam mais com o cluster, resultando em maiores acessos de leitura/gravação por segundo. Se o pico diário de leituras atingir 1.000 RCU/s, o pico diário de gravação 300 WCU/s e o pico diário de dados 1,5 GB, as taxas diárias serão calculadas da seguinte forma:

| Capacidade (GB) | Solicitações de leitura (RCU) |  Solicitações de gravação (WCU)  | Taxas |
|---------|---------|---------|-------|
| 1,5 | 1.000 |  300 | 1,5 GB × 0,0052 USD/GB/dia + 1.000 RCUs × 0,0019 USD/RCU/dia + 300 WCUs × 0,0048 USD/WCU/dia = 3,3478 USD |


## Regras de faturamento para a edição de cluster autoimplantado
A edição de cluster autoimplantado adota o modo de faturamento com pagamento conforme o uso. As taxas diárias são calculadas com base nos recursos realmente usados nas camadas de armazenamento e nas camadas de acesso em um dia.

**Taxas diárias = Preço unitário diário da camada de acesso × Quantidade da camada de acesso + Preço unitário diário da camada de armazenamento (que varia com o tipo de instância) × Quantidade da camada de armazenamento**

### Preços
| Região| Camada de acesso (USD/camada/dia) | Instância padrão T1 Uma-principal-Uma-secundária na camada de armazenamento (USD/instância/dia) |
|---------|---------|---------|
| China Continental| 0,51 | 65,22 |
|   Virgínia (Leste dos Estados Unidos)  |1,52| 220,58 |
|   Vale do Silício (Oeste dos Estados Unidos)  |1,57| 224,49 |
|Frankfurt (Alemanha)| 1,57 | 224,49 |
|  Singapura |1,89 | 224,49 |
|   Hong Kong (China)  | 1,89 |226,38 |
|   Japão  | 1,76 | 226,38 |
|Seul | 1,76 |222,03 |

### Amostra de faturamento
Suponha que você crie um cluster autoimplantado na região de Xangai. O cluster tem quatro camadas de acesso e duas camadas de armazenamento (ou seja, duas instâncias padrão T1 uma-principal-uma-secundária).
As taxas diárias são calculadas da seguinte forma:

Taxas diárias da camada de acesso = 0,5 × 4 = 2 USD/dia
Taxas diárias da camada de armazenamento = 64,28471429 × 2 = 128,56942858 USD/dia

Taxas diárias totais = 2 + 128,56942858 = 130,56942858 USD/dia
