Tencent Cloud Log Service (CLS) allows you to **save about 84%** on your budget compared with the self-built logging system (for example, ELK) of Elasticsearch Service. A detailed comparison is given herein.

## Cost Comparison
The following table compares the costs with an assumption that 100 million pieces of 100-byte logs are generated per day, all logs need to be stored for 15 days, and the peak QPS is 4,000:

| Product | List Price | Description |
|---------|---------|---------|
| CLS | 38 USD/month |  <ul  style="margin: 0;"><li>Write traffic: 0.074 USD/day<br /> </li><li>Index traffic: 0.694 USD/day<br /> </li><li>Log storage: 0.084 USD/day<br /> </li><li>Index storage: 0.403 USD/day<br /> </li><li>Service request: 0.003 USD/day<br /> </li><li>Topic partition tenant: 0.014 USD/day<br />For more information, please see the <b>Billing Example</b> section in [Billing Overview](https://intl.cloud.tencent.com/document/product/614/37509). |
| Self-built logging system of the Elasticsearch Service | 244 USD/month | <li>Node model: 125 USD/month<br /> <li>Node storage: 119 USD/month |

## Billing Description

Elasticsearch involves the following fees:
**Node model fees**
125 USD/month (assume that you purchased the ES.S1.MEDIUM8 model with a 2-core CPU and 4 GB memory for the three nodes)

**Node storage fees**
 - According to the [Elasticsearch Service](https://intl.cloud.tencent.com/document/product/845/19551) documentation, using 1 replica improves data reliability, and reserving 50% of the storage capacity maintains service stability. In this case, the actual storage will be as follows:
 - Actual capacity:
   Storage capacity = Source data × (1 + Number of replicas) × 1.45 × (1 + reserved capacity) ​≈ Source data × (1 + Number of replicas) × 2.2 = 614.46 GB
   If you use a 210 GB SSD for each node, the three nodes will cost 119 USD per month.
>?For more information about cluster configurations, please see [Evaluation of Cluster Specification and Capacity Configuration](https://intl.cloud.tencent.com/document/product/845/19551).





