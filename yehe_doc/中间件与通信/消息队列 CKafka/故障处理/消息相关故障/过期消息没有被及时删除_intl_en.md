## Issue Description

Expired messages are not deleted promptly.

## Cause Analysis

The message deletion mechanism of Kafka may cause a problem where expired messages are not deleted promptly in certain business scenarios. You may feel confused if you are unfamiliar with this mechanism. The specific problem is as follows:

Here, the message timestamps in partition 0 and partition 7 are obviously different, and expired messages in partition 0 are not deleted promptly as shown below:

- Partition 0:
  ![](https://qcloudimg.tencent-cloud.cn/raw/59e9fde4aa856843b6cd6fba8af95c54.png)
- Partition 7:
  ![](https://qcloudimg.tencent-cloud.cn/raw/3b15267560e955a28743d94d6d007245.png)

## Kafka Message Deletion Mechanism

Kafka data is stored in three dimensions: topic, partition, and data segment. The message data deletion conditions are as follows:

- Message data is deleted by data segment based on the retention period.
- Currently, the maximum size of a data segment is set to 1 GB. After a data segment reaches 1 GB in size, a new segment will be generated, and so on.
- Only after all messages in a data segment expire will the segment be deleted.
- If a message in a data segment is still within the retention period, such as the last row of a segment file, then the file will not be deleted.

For some reasons, messages are written unevenly and concentrated in a certain partition (such as partition 7), and some other partitions (such as partition 0) have only little data. In this case, the size of the data segment in partition 0 does not reach 1 GB, so no new segments are generated; however, there is data within the retention period in the entire data segment. Therefore, messages in partition 0 will not be deleted.

