In TDSQL-C for MySQL, there are two different types of prepaid resource packs: compute resource packs and storage resource packs, which can be used to deduct the storage and compute resources used by the serverless cluster. By purchasing resource packs, you can reserve resources in advance. Compared to the pay-as-you-go option, the resource packs can help you save more costs. It is more cost-effective to purchase larger capacity and longer validity period.
## Resource Pack Description
| Prepaid Resource Pack | Compute Resource Pack |Storage Resource Pack |
| ---- | ---- | --- |
| Deduction object | The compute resource pack will be used preferably for the deduction of actual compute resources used by its bound severless cluster. When the pack is used up, the resource usage will be pay-as-you-go. | The storage resource pack will be used preferably for the deduction of actual storage resources used by its bound severless cluster. When the pack is used up, the resource usage will be pay-as-you-go. |
| Deduction rules | The compute resource pack will be deducted based on the actual CCU usage per second, which is more cost-effective and flexible than the pay-as-you-go option. Before the deduction of the serverless cluster, you must first bind a resource pack. The cluster will not be terminated when the resource pack is unbound, used up, or expires. It will instead be billed on a pay-as-you-go basis. | The storage resource pack will be deducted based on the actual storage used per hour, which is more cost-effective and flexible than the pay-as-you-go option. Before the deduction of the serverless cluster, you must first bind a resource pack. The cluster will not be terminated when the resource pack is unbound, used up, or expires. It will instead be billed on a pay-as-you-go basis. |
| Renewal | Not supported | | Not supported |
| Deduction period | The compute resource pack will be deducted based on the actual accumulated usage per second. |The storage resource pack will be deducted based on the actual average usage per hour. |
| Validity period | It is valid for 6 months (180 days) or 1 year (365 days) and can’t be used any longer once expired. | It is valid for 6 months (180 days) or 1 year (365 days) and can’t be used any longer once expired. |
| Region | It is available in or out of the Chinese mainland. | It is available in or out of the Chinese mainland. |
| Use Instructions | <li>[Purchasing Resource Pack](https://www.tencentcloud.com/document/product/1098/55247)</li><li>[Binding and Unbinding Resource Pack](https://www.tencentcloud.com/document/product/1098/55250)</li> |<li>[Purchasing Resource Pack](https://www.tencentcloud.com/document/product/1098/55247)</li><li>[Binding and Unbinding Resource Pack](https://www.tencentcloud.com/document/product/1098/55250)</li>|

## Available Region
| In Chinese Mainland | Outside Chinese Mainland | 
|---------|---------|
| Guangzhou, Nanjing, Shanghai, Beijing, Chengdu, Chongqing, Beijing Finance, Shanghai Finance | Hong Kong (China), Singapore, Seoul, Tokyo, Silicon Valley, Virginia, Toronto, Frankfurt |

## Billing Mode
Serverless clusters offer the following four billing modes for you to choose flexibly. If you choose the fourth mode of **resource pack for both compute and storage**, you can enjoy a more favorable price than the monthly subscription option.
- Pay-as-you-go for compute + resource pack for storage
- Resource pack for compute + pay-as-you-go for storage
- Pay-as-you-go for both compute and storage
- Resource pack for both compute and storage

For more information, see [Compute Resource Pack](https://www.tencentcloud.com/document/product/1098/55248) and [Storage Resource Pack](https://www.tencentcloud.com/document/product/1098/55249).









