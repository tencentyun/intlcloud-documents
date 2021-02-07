The CKafka service can be billed as an instance using a **prepaid monthly subscription** plan.

## Standard Edition

Currently, CKafka Standard Edition has 2 versions available in 8 instance types such as small and standard based on **peak throughput** and **disk capacity**. Disks can be expanded separately.
CKafka has an elastic and cost-effective billing mode that only requires you to estimate the performance and disk capacity required by your business and purchase instances as needed. Instances are deployed in the multi-node cluster mode, allowing you to enjoy highly reliable and available services without having to worry about the underlying deployment.

>?
>- Throughput refers to the outbound and inbound bandwidth. For example, a throughput of 40 MB indicates that the outbound and inbound peak bandwidth is 40 MB. The replicas of an instance share the throughput equally. For example, for a throughput of 40 MB and three replicas, you should purchase a bandwidth with a throughput of 120 MB/s.
>- For more information on conditions that may affect the data reliability of CKafka, please see [CKafka Data Reliability](https://intl.cloud.tencent.com/document/product/597/31586).


### Standard Edition instance pricing

**Standard Edition pricing**

| Instance Type | Peak Throughput (MB/s) | Disk Capacity (GB) | Number of Instance-Level Topics | Number of Instance-Level Partitions | Price (USD/Month) |
| -------- | ------------------ | -------------- | ----------------- | --------------------- | ------------- |
| Small   | 40                 | 300            | 25                | 60                    | 870           |
| Standard   | 100                | 1000           | 40                | 100                   | 1510          |
| Advanced   | 150                | 2500           | 50                | 150                   | 1920          |
| Large   | 180                | 4000           | 150               | 300                   | 2330          |
| Xlarge L1 | 300                | 6000           | 250               | 500                   | 2740          |
| Xlarge L2 | 400                | 6000           | 250               | 500                   | 3970          |
| Xlarge L3 | 600                | 6000           | 350               | 600                   | 5170          |
| Xlarge L4 | 900                | 9000           | 450               | 700                   | 7030          |
| Dedicated   | 1200               | 24000          | 1000              | 1500                  | 13900         |


>?
>
>- One topic can support up to 24 partitions.
>- A maximum of 50 instance-level consumer groups is supported by default.
>- The instance-level partition limit applies to the number of replicas. For example, if an instance has one topic with 2 replicas with 4 partitions each, and two topics with 3 replicas with 3 partitions each, then the total number of partitions in this instance is (1 * 2 * 4) + (2 * 3 * 3) = 26.
>- An idle consumer group can exist for up to 7 days.
>- If you need CKafka instances with higher specifications, please contact your Tencent Cloud rep or [submit a ticket](https://intl.cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory) for assistance.

### Disk expansion pricing

| Instance Type | Disk Capacity (GB) | Price (USD/Month) |
| --------------- | -------------- | ------------- |
| Shared - disk expansion | 100            | 8           |