## Billing Method
 - TencentDB for Redis uses a linear pricing strategy, where the charges for an instance is calculated by multiplying the instance specifications by the unit price.
 - It is pay-as-you-go.
 - The billable usage time is accurate down to the second, where the unit price = monthly price / 30 days / 24 hours / 3600 seconds.


### Pay-as-you-go
TencentDB for Redis supports tiered pricing. The longer it is used, the cheaper it is.
Depending on the usage duration, the prices in pay-as-you-go mode are divided into three tiers:
- 0 days < duration ≤ 4 days: Tier 1 pay-as-you-go pricing is used, where hourly price = monthly price / 30 / 24 * 2
- 4 days < duration ≤ 15 days: Tier 2 pay-as-you-go pricing is used, where hourly price = monthly price / 30 / 24 * 1.5
- Duration > 15 days: Tier 3 pay-as-you-go pricing is used, where hourly price = monthly price / 30 / 24


| Configuration | USD/GB/Hour | USD/GB/Month | Region |
|---------|---------|---------| --------- |
|1 GB MEM|	0.034704|	24.98688|	Beijing, Shanghai, Guangzhou, Chengdu, and Chongqing |
|1 GB MEM|0.029196|21.02112|East US (Virginia) and West US (Silicon Valley) |
|1 GB MEM|	0.036108|	25.99776|	Hong Kong (China) and Singapore |
|1 GB MEM|	0.045792|	32.97024|	Mumbai |
|1 GB MEM|	0.037512|	27.00864|	Seoul |
|1 GB MEM|	0.041688| 30.01536|	Frankfurt |
|1 GB MEM|	0.024984|	17.98848|	Moscow |
|1 GB MEM|	0.045792| 32.97024|	Bangkok |
|1 GB MEM|	0.026388|	18.99936|	Tokyo |
|1 GB MEM|	0.050004|	36.00288|	North America |

> After an instance is scaled or isolated, it will be billed based on the tier 1 pricing.

