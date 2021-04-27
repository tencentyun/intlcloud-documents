## Billing Modes
>? Monthly subscription is currently in beta. This pricing document is for reference only, please see your bill for the actual price. If you wish to use this billing option, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>
- TencentDB for Redis adopts a linear pricing strategy, where charges for an instance are calculated by multiplying the instance specifications by the unit price.
- TencentDB for Redis provides two billing options, pay-as-you-go and monthly subscription.
- For pay-as-you-go, the billable usage time is accurate down to the second, where the unit price = monthly price / 30 days / 24 hours / 3600 seconds.



### Pay-as-you-go

TencentDB for Redis supports tiered pricing. The longer you use it, the more you save.
The tiered pricing model is based on usage duration.

- 0 days < duration ≤ 4 days: Tier 1 pay-as-you-go pricing applies, where hourly price = monthly price / 30 / 24 * 2
- 4 days < duration ≤ 15 days: Tier 2 pay-as-you-go pricing applies, where hourly price = monthly price / 30 / 24 * 1.5
- Duration > 15 days: Tier 3 pay-as-you-go pricing applies, where hourly price = monthly price / 30 / 24

| Configuration | USD/GB/Hour | USD/GB/Month | Region |
| :------ | :----------- | :--------- | :-------------------------------- |
| 1 GB MEM | 0.034704 | 24.98688 | Beijing, Shanghai, Guangzhou, Chengdu, and Chongqing |
| 1 GB MEM | 0.029196 | 21.02112 | US East Coast (Virginia) and West Coast (Silicon Valley) |
| 1 GB MEM | 0.036108 | 25.99776 | Hong Kong (China) and Singapore |
| 1 GB MEM | 0.045792 | 32.97024 | Mumbai |
| 1 GB MEM | 0.037512 | 27.00864 | Seoul |
| 1 GB MEM | 0.041688 | 30.01536 | Frankfurt |
| 1 GB MEM | 0.024984 | 17.98848 | Moscow |
| 1 GB MEM | 0.045792 | 32.97024 | Bangkok |
| 1 GB MEM | 0.026388 | 18.99936 | Tokyo |
| 1 GB MEM | 0.050004 | 36.00288 | North America |

> Note:
>
> Prices revert to tier 1 for instances that are scaled or isolated.

### Monthly subscription

An upfront payment is required for monthly subscription instances.

For specific pricing details, please see [Product Pricing](http://intl.cloud.tencent.com/document/product/583/12281)
