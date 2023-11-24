### Visão geral

A instância reservada (Reserved Instance, RI) é um desconto no faturamento aplicado ao uso de instâncias do CVM com pagamento conforme o uso em sua conta. Essas instâncias do CVM devem corresponder exatamente aos atributos da RI que você adquiriu para se beneficiar do desconto no faturamento durante o período de vigência da RI. A RI oferece um desconto significativo em comparação ao faturamento com pagamento conforme o uso.
>? 
>- Faça login no console do Tencent Cloud e acesse a [Calculadora de preços](https://intl.cloud.tencent.com/pricing/cvm) para consultar o preço.

>- Atualmente, as RIs não são reembolsáveis.
>
>- As configurações de uma RI não podem ser alteradas após a aquisição. O desconto no faturamento da RI não se aplicará mais à instância correspondente se você alterar as configurações dela.
>
>- O desconto no faturamento da RI ainda se aplicará às instâncias do CVM correspondentes, mesmo depois de serem desligadas de forma proativa ou forçada.

#### Atributos

- [Região](https://intl.cloud.tencent.com/document/product/213/6091): a localização física de um IDC, como o Vale do Silício.
- [Zona de disponibilidade](https://intl.cloud.tencent.com/document/product/213/6091): um IDC do Tencent Cloud com fonte de alimentação e rede independentes na região acima, como a Zona 1 do Vale do Silício.
- [Tipo de instância](https://intl.cloud.tencent.com/document/product/213/11518): um tipo de família de instâncias do Tencent Cloud CVM, como Padrão.
- [Especificação](https://intl.cloud.tencent.com/document/product/213/11518): especificações da RI, como S4.SMALL. 
- Sistema operacional: Linux OS

> As instâncias do CVM com pagamento conforme o uso devem corresponder exatamente aos atributos da RI para se beneficiar do desconto no faturamento durante o período de vigência da RI.

#### Comparação de conceitos

| Item   | RI      | Instância com pagamento conforme o uso         |
| -------- | ---------- | ---------- |
| Conceito     | Um desconto para as instâncias com pagamento conforme o uso.       | Uma instância adquirida usando a opção de faturamento [com pagamento conforme o uso](https://intl.cloud.tencent.com/document/product/213/2179), ou seja, uma máquina virtual em execução. |
| Uso | As RIs não podem ser usadas separadamente; em vez disso, elas só podem ser usadas com as instâncias com pagamento conforme o uso correspondentes, para compensar parte da fatura com pagamento conforme o uso. | Os CVMs podem ser gerenciados e configurados de forma independente, como um servidor web simples ou como parte de uma solução avançada de nuvem junto com outros produtos do Tencent Cloud. |

#### Limites de uso

Para verificar as zonas de disponibilidade compatíveis com as RIs, use a API [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575).

Sistema operacional: atualmente, apenas as instâncias do CVM do Linux são compatíveis com a RI.

Método de pagamento: existem dois opções de pagamento: Pagamento total adiantado, Pagamento parcial adiantado .

Períodos de vigência: 1 ano(365 dias)

Cota: cada usuário pode ter até 20 RIs em uma zona de disponibilidade.
