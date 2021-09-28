## What should I do if consumption is exceptional?

- You can view the traffic monitoring data on the monitoring page in the CKafka console to check whether there is a surge, and if so, upgrade the instance specification for solution.

  ![](https://main.qcloudimg.com/raw/a5ef5e5067c265073ef8cb0c07960461.png)

- Check whether the number of consumer groups exceeds the limit.

- If rebalance occurs frequently for network reasons, we recommend you adjust the client timeout period.

- Check whether expired offsets are pulled. Messages will be deleted after expiration, and if they are pulled with expired offsets, the pull will fail.

## What should I do if an error persists after a period of production?

- View whether traffic throttling is performed. Check whether there is a surge in traffic on the monitoring page and upgrade the instance specification for solution.
- View whether capacity throttling is performed. Check the instance disk capacity on the monitoring page and upgrade the instance specification or modify the data retention period for solution.

## How do I calculate the number of unconsumed messages?

Number of unconsumed messages = maximum offset - submitted offset, as shown below:

![img](https://main.qcloudimg.com/raw/05c88d97f36784e5f83c08b24e229265.png)



## Why aren't expired messages deleted promptly?

The message deletion mechanism of Kafka may cause a problem where expired messages are not deleted promptly in certain business scenarios. You may feel confused if you are unfamiliar with this mechanism. The specific problem is as follows:

Here, the message timestamps in partition 0 and partition 7 are obviously different, and expired messages in partition 0 are not deleted promptly as shown below:
- Partition 0:
![](https://main.qcloudimg.com/raw/15259a044edd174cbe609a9a95e43ea2.png)
- Partition 7:
![](https://main.qcloudimg.com/raw/bda384e0ed20e043f9416481e6d6d2a5.png)

**Kafka message deletion mechanism**

Kafka data is stored in three dimensions: topic, partition, and data segment. The message data deletion conditions are as follows:

1. Message data is deleted by data segment based on the retention period.
2. Currently, the maximum size of a data segment is set to 1 GB. After a data segment reaches 1 GB in size, a new segment will be generated, and so on.
3. Only after all messages in a data segment expire will the segment be deleted.
4. If a message in a data segment is still within the retention period, such as the last row of a segment file, then the file will not be deleted.

For some reasons, messages are written unevenly and concentrated in a certain partition (such as partition 7), and some other partitions (such as partition 0) have only little data. In this case, the size of the data segment in partition 0 does not reach 1 GB, so no new segments are generated; however, there is data within the retention period in the entire data segment. Therefore, messages in partition 0 will not be deleted.



## Can the message retention period be automatically adjusted?

CKafka allows you to add dynamic message retention policies. After such a policy is set, if the disk utilization reaches the specified percentage, a certain proportion of existing data will automatically expire in case of message surges, helping avoid situations where normal production and consumption stop after the disk space is used up. For detailed directions, please see [Adding Dynamic Message Retention Policy](https://intl.cloud.tencent.com/document/product/597/40211).
