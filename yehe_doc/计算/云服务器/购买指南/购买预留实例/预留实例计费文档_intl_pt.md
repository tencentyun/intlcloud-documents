### Visão geral

A oferta de instância reservada é um desconto no faturamento aplicado ao uso de instâncias do CVM com pagamento conforme o uso em sua conta. A RI se aplica automaticamente às instâncias com pagamento conforme o uso em execução com atributos correspondentes, portanto, essas instâncias se beneficiarão do desconto durante o período de vigência da RI. Você pode adquirir e ativar uma RI para o seu CVM atual ou comprar uma antes mesmo de adquirir um CVM. As RIs fornecem flexibilidade e economia significativa em comparação com os modos de faturamento com pagamento conforme o uso.

**Produtos compatíveis**

CVM

**Aquisição de RIs**

- As RIs permitem que você escolha o tipo de CVM mais adequado às suas necessidades e ao seu orçamento. Você pode escolher o tipo (modelo e configuração), o método de pagamento, a região, o período de vigência e a quantidade da sua RI.

- Atualmente, você pode adquirir RIs por API ou pelo console do Tencent Cloud. Para obter mais informações, consulte a [Documentação do CVM](https://intl.cloud.tencent.com/document/product/213).

- As RIs não são reembolsáveis.

**Preços e tipos de instâncias compatíveis com a RI**
Para obter mais informações sobre as configurações, as regras de correspondência e os preços dos tipos de instância compatíveis com a RI, consulte a [Documentação do CVM](https://intl.cloud.tencent.com/document/product/213).
Para obter mais informações sobre as zonas de disponibilidade e os tipos de instância compatíveis com a RI, consulte os [Preços do CVM](https://intl.cloud.tencent.com/pricing/cvm) ou a API [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575). 
Para obter mais informações, consulte as [regras de correspondência da RI](https://intl.cloud.tencent.com/document/product/213/37265) e a [Visão geral da instância reservada](https://intl.cloud.tencent.com/document/product/213/30571).
O CVM é compatível com a RI. Para obter mais informações sobre o preço, consulte a [Visão geral dos preços de instância reservada do CVM (Linux)](https://intl.cloud.tencent.com/document/product/213/30619). 

**Métodos de pagamento**

- All Upfront (Pagamento total adiantado): você paga por todo o período de vigência da RI com um pagamento adiantado. Esta opção oferece o maior desconto em comparação com as outras duas opções abaixo.

- Partial Upfront (Pagamento parcial adiantado): você faz um pagamento inicial baixo e, depois, paga as taxas da instância a uma tarifa mensal ou tarifa horária com desconto durante o período de vigência da RI.

S- No Upfront (Sem pagamento adiantado): você não faz nenhum pagamento inicial e, depois, paga as taxas da instância a uma tarifa mensal ou tarifa horária com desconto durante o período de vigência da RI.

Observe que você paga por todo o período de vigência da RI, independentemente do uso real.

**Períodos de vigência**

1 ano(365 dias)

Suponha que você adquiriu uma RI do CVM com período de vigência de 1 ano em 25 de maio de 2019 às 11:15:24, a RI será válida de 25 de maio de 2019 às 11:00:00 a 25 de maio de 2020 às 11:59:59.

Observação: as instâncias com pagamento conforme o uso correspondentes continuam a ser executadas quando a RI expira, mas o desconto no faturamento é interrompido.

**Regras de faturamento**

- As RIs são faturadas a cada hora cheia (3.600 segundos) durante o período de vigência que você escolher. Por exemplo, 10:00:00 a 10:59:59 corresponde a uma hora cheia. O benefício de faturamento da RI pode ser aplicado a várias instâncias elegíveis ao mesmo tempo, até um máximo de 3.600 segundos em uma hora cheia. Você encontra o detalhamento na sua fatura.

- As RIs são faturadas a cada hora durante o período de vigência escolhido, independentemente de corresponder a uma instância com pagamento conforme o uso. Portanto, é importante escolher uma opção de pagamento adequada com base no seu orçamento e recursos. As RIs entram em vigor na hora anterior da hora de criação e expiram na próxima hora da hora de expiração. Por exemplo, se você adquirir uma RI do CVM com período de vigência de 1 ano em 25 de maio de 2019 às 11:15:24, o faturamento da RI começará a partir de 25 de maio de 2019 às 11:00:00 e terminará em 25 de maio de 2020 às 11:59:59. Se você já tiver recursos do CVM correspondentes no momento da aquisição, o primeiro ciclo de faturamento da RI será das 11:00:00 às 11:59:59 do dia 25 de maio de 2019, e será faturado a cada hora cheia.

**Desconto da RI:**

desconto no faturamento recebido quando uma RI adquirida é correspondente a uma instância compatível.
