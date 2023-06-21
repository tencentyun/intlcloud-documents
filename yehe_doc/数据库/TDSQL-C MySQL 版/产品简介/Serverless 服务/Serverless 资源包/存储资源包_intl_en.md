The storage resource pack is a prepaid resource type in TDSQL-C for MySQL, which can be used to deduct the storage resources used by the serverless cluster. This document describes the specification types and prices of storage resource packs.
## Specification Types and Prices
| Specification Type | Applicable Scope of Storage Capacity | Reference Usage Period | Unit Price in Chinese Mainland (USD/TB) | Unit Price Outside Chinese Mainland (USD/TB) |
| ---- | ---- |---|---|---|
| Basic Edition | 2–⁠200TB (200 exclusive) | 90 days for a database with 1–100 GB storage | 6-month validity period: 0.2568 <br>1-year validity period: 0.271 | 6-month validity period: 0.2806 <br>1-year validity period: 0.2962 |
| General Edition | 200–2000 TB (2000 exclusive) | 90 days for a database with 100 GB–1 TB storage | 6-month validity period: 0.2425 <br>1-year validity period: 0.2568 | 6-month validity period: 0.265 <br>1-year validity period: 0.2806 |
| Enterprise Edition | 2000–20,000 TB (20,000 exclusive) | 90 days for a database with 1 TB–10 TB storage | 6-month validity period: 0.2282 <br>1-year validity period: 0.2425 | 6-month validity period: 0.2494 <br>1-year validity period: 0.265 |

## Note
The storage resource pack will be deducted based on the actual storage used per hour, which is more cost-effective and flexible than the pay-as-you-go option. Before the deduction of the serverless cluster, you must first bind a storage resource pack. The cluster will not be terminated when the resource pack is unbound, used up, or expires. It will instead be billed on a pay-as-you-go basis. It is important to note the following points:
- Storage resource packs are classified into two types: those for the Chinese mainland and those for regions outside the Chinese mainland. Each type is specified to be shared by all serverless clusters in the region, that is, one storage resource pack can be shared by multiple serverless clusters.
- A serverless cluster can only be bound to one storage resource pack.
- A storage resource pack is deducted based on the actual usage per hour.
- A storage resource pack doesn’t support downgrade once purchased.

## Management
- [Binding and Unbinding Resource Pack](https://cloud.tencent.com/document/product/1003/92592)
- [Viewing Resource Pack Usage](https://cloud.tencent.com/document/product/1003/92593)
- [Modifying Resource Pack Name](https://cloud.tencent.com/document/product/1003/92594)

## Refund
After purchasing storage resource packs, each Tencent Cloud root account can make up to 20 refund requests for the storage resource packs. For more information, see [Requesting Refund for Resource Pack](https://cloud.tencent.com/document/product/1003/92595).

## Relevant Documents
- [Compute Resource Pack](https://cloud.tencent.com/document/product/1003/92589)
- [Purchasing Resource Pack](https://cloud.tencent.com/document/product/1003/92591)

