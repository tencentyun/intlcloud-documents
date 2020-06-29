### Pricing

 The pricing of postpaid CKafka is determined by the throughput unit and number of messages (in millions): 

- Throughput unit (1 MB/s): 0.36 USD/day
- Number of messages in millions: 0.028 USD per 1,000,000 messages (price is accurate to three decimal places. Please refer to your bill for the exact price).

## Prepaid Pricing

The CKafka can be billed as an instance with **prepaid monthly subscription**.

Currently, CKafka has 9 instance types including small, standard, and dedicated based on **peak throughput** and **disk capacity**. Disk can be expanded separately.
CKafka has an elastic and cost-effective billing mode. You only need to estimate the performance and disk capacity required by your business and purchase instances as needed, which are deployed using the multi-node cluster mode. You can enjoy reliable and available services without worrying about the underlying deployment.

>
- Throughput refers to the outbound and inbound bandwidth. For example, a throughput of 40 MB indicates that the outbound and inbound peak bandwidth is 40 MB. The replicas of an instance share the throughput equally. For example, for a throughput of 40 MB and three replicas, you should purchase a bandwidth with a throughput of 120 MB/s.
- For more information on conditions that may affect the data reliability of CKafka, see [CKafka Data Reliability Description](https://intl.cloud.tencent.com/document/product/597/31586).
- Shared instances cannot be directly upgraded to dedicated instances. For more information, please see [Migrating Data to CKafka](https://intl.cloud.tencent.com/document/product/597/17272). If you need dedicated instances, please contact your Tencent Cloud sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CKafka&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) for assistance.


<span id="standard"></span>
### Pricing of standard instances

| Instance Type | Peak Throughput (MB/s) | Disk Capacity (GB) | Number of Instance-Level Topics | Number of Instance-Level Partitions | Price (USD/month) |
|---------|---------|-----|------|--------|------|
| Small | 40 | 300 | 25| 60 | 870 |
| Standard | 100 | 1,000 | 40 | 100 | 1,510 |
| Advanced | 150 | 2,500 | 50 | 150 | 1,920 |
| Large |  180 |4,000 | 150| 300|2,330 |
| Xlarge L1 |  300 |6,000 | 250| 500|2,740 |
| Xlarge L2 |  400 |6,000 | 250| 500|3,970 |
| Xlarge L3 |  600 |6,000 | 350| 600|5,170 |
| Xlarge L4 |  900 |9,000 | 450| 700|7,030 |
| Dedicated |  1,200 |24,000 | 1,000| 1,500|13,900 |

>- One topic can support up to 24 partitions.
- A maximum of 50 instance-level consumer groups is supported by default.
- The instance-level partition limit applies to the number of replicas. For example, if an instance has one topic with 2 replicas and each with 4 partitions, and two topics with 3 replicas and each with 3 partitions, the total number of partitions in this instance is (1 * 2 * 4) + (2 * 3 * 3) = 26.
- An idle consumer group can exist for up to 7 days.
- If you need CKafka instances with higher specifications, please contact your Tencent Cloud sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Pricing of disk expansion
| Instance Type | Disk Capacity (GB) | Price (USD/month) |
|---------|-----|------|
| Shared - disk expansion |100|8|