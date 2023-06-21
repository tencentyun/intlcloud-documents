The compute resource pack is a prepaid resource type in TDSQL-C for MySQL, which can be used to deduct the compute resources used by the serverless cluster. This document describes the specification types and prices of compute resource packs.
## Specification Types and Prices
| Specification Type | Applicable Scope of CCU | Reference Usage Period | Unit Price in Chinese Mainland (USD/Thousand CCU) | Unit Price Outside Chinese Mainland (USD/Thousand CCU) |
| ---- | ---- |---|---|---|
| Basic Edition | 400–⁠10,000 thousand CCU (10,000 exclusive) | For a 2-core-4 GB MEM database, full load usage lasts about 60 days and non-full load usage lasts up to 300 days. | 6-month validity period: 0.0119 <br>1-year validity period: 0.0126 | 6-month validity period: 0.013 <br>1-year validity period: 0.0138 | 
| General Edition | 10,000–⁠40,000 thousand CCU (40,000 exclusive) | For a 8-core-16 GB MEM database, full load usage lasts about 60 days and non-full load usage lasts up to 300 days. | 6-month validity period: 0.0112 <br>1-year validity period: 0.0119 | 6-month validity period: 0.0122 <br>1-year validity period: 0.013 | 
| Enterprise Edition | 40,000–200,000 thousand CCU (200,000 exclusive) | For a 32-core-64 GB MEM database, full load usage lasts about 60 days and non-full load usage lasts up to 300 days. | 6-month validity period: 0.0105 <br>1-year validity period: 0.0112 | 6-month validity period: 0.0115 <br>1-year validity period: 0.0122 |

## Note
The compute resource pack will be deducted based on the actual CCU usage per second, which is more cost-effective and flexible than the pay-as-you-go option. Before the deduction of the serverless cluster, you must first bind a compute resource pack. The cluster will not be terminated when the resource pack is unbound, used up, or expires. It will instead be billed on a pay-as-you-go basis. It is important to note the following points:
- Compute resource packs are classified into two types: those for the Chinese mainland and those for regions outside the Chinese mainland. Each type is specified to be shared by all serverless clusters in the region, that is, one compute resource pack can be shared by multiple serverless clusters.
- A serverless cluster can only be bound to one compute resource pack.
- A compute resource pack is deducted based on the accumulated usage per second.
- A compute resource pack doesn’t support downgrade once purchased.

## Management
- [Binding and Unbinding Resource Pack](https://cloud.tencent.com/document/product/1003/92592)
- [Viewing Resource Pack Usage](https://cloud.tencent.com/document/product/1003/92593)
- [Modifying Resource Pack Name](https://cloud.tencent.com/document/product/1003/92594)

## Refund
After purchasing compute resource packs, each Tencent Cloud root account can make up to 20 refund requests for the compute resource packs. For more information, see [Requesting Refund for Resource Pack](https://cloud.tencent.com/document/product/1003/92595).

## Relevant Documents
- [Storage Resource Pack](https://cloud.tencent.com/document/product/1003/92590)
- [Purchasing Resource Pack](https://cloud.tencent.com/document/product/1003/92591)

