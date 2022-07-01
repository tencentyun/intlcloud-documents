## Billing Mode

CDWPG is pay-as-you-go service that charges you by the nodes you use. For more information on pay-as-you-go billing, see [Postpaid Billing](https://intl.cloud.tencent.com/document/product/555/30328).

## Pricing

CDWPG nodes can be compute-intensive, storage-intensive, or storage-elastic.

·    Storage-elastic models come with flexible node specifications, disk types, and disk capacities, suitable for scenarios with high storage requirements and demanding a strong storage scalability in the future.

### Pricing of storage-elastic models

Total cluster fees = single node fees (node specification fees + node storage fees) * number of nodes

#### Node specification

The supported regions and pay-as-you-go prices are as follows:

| Specification Type | CPU (Cores) | Memory (GB) | Japan (USD/Node/Hour) | Virginia (USD/Node/Hour) |
| -------- | --------- | ---------- | ------------ |------------ |
| 4C16G    | 4         | 16         | 0.336   |       0.252   |
| 8C32G    | 8         | 32         | 0.644    |       0.504   |
| 16C64G   | 16        | 64         | 1.288   |        0.994   |

#### Node storage

Pay-as-you-go prices in Japan and Virginia are as follows:

| **Disk Type** | Japan (USD/GB/Hour) | Virginia (USD/GB/Hour) |
| ------------ | ---------- | ---------- |
| Enhanced SSD   | 0.0003       | 0.0003       |
| Premium Cloud Storage   |0.0001       | 0.0001       |

If you need special models, [contact us](https://intl.cloud.tencent.com/contact-us) for assistance.

## Fees Calculation Examples

CDWPG is a distributed cluster deployed in a VPC, typically consisting of two or more nodes.

**Total cluster fees = single node fees * number of nodes**

### Pay-as-You-Go

**Example:** If you purchase a CDWPG cluster with two compute nodes (4 CPU cores, 16 GB memory, and 100 GB enhanced SSD storage) in Japan in pay-as-you-go mode, you should pay hourly in CNY/second:

Hourly fees: (m + n * 100) * 2 = 0.732 USD/hour.  
