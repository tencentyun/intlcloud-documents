## Billing mode
ES is billed on a pay-as-you-go basis.

## Billable items
ES is a distributed cluster deployed in VPC which typically consists of 3 or more nodes. Each node contains computing resources (available with specified CVM models) and storage resources (SSD/premium cloud disk with a certain storage capacity).

**Total fees for a cluster** = **Fees per node** (compute fees + storage fees) \* **number of nodes**
![](https://main.qcloudimg.com/raw/905a5aec524cfbda86786e2afc3bca68.png)

### Node

#### Compute (node model)
Hardware devices of different specifications come with different computing capabilities to meet the diverse requirements for cluster write and query performance. In addition, ES offers multiple editions of **Elastic Stack**. Specifically, the Basic Edition and Platinum Edition contain Elasticsearch's official commercial features (formerly X-Pack). The pricing of node models varies by the **Elastic Stack** edition. For more information, see [Product Pricing](https://intl.cloud.tencent.com/document/product/845/18376).

#### Storage
ES currently uses SSD and premium cloud disks as the storage media for ES clusters to ensure overall performance of data writes, queries, and reads as well as data security.

Suggestions for disk capacity:
- ES is a distributed cluster consisting of multiple nodes, and the storage of such nodes constitutes the total data capacity of the cluster. You can select the disk capacity based on your assessment of the total data volume and number of nodes. 
- When storing an index, you can ensure the high availability of the cluster by specifying a certain number of replicas and improve query performance by deploying multiple nodes in a distributed manner.
- A certain amount of disk capacity is required for cluster running, and a certain buffer is required to ensure cluster stability.

#### Pricing
For more information on pricing, see [Product Pricing](https://intl.cloud.tencent.com/document/product/845/18376).
