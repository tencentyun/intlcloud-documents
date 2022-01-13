## Issue Description
A consumer group is constantly in `PreparingRebalance` status.


## Possible Causes
1. A new consumer joins the consumer group.
2. A running consumer stops running and leaves the consumer group. Common causes for this include consumer restart, consumer application crash, and heartbeat timeout of consumer process reporting. For more information, see [Configuration Guide for Common Parameters in CKafka](https://intl.cloud.tencent.com/document/product/597/31588).
3. The number of partitions changes (partitions are added or deleted).




## Solutions

Rebalancing is inevitable in cases 1 and 3. Normally, rebalancing can be completed in 30s. If there is a longer rebalancing process, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

If the rebalancing is caused by heartbeat timeout or excessive interval between two polls, you can adjust the following parameters:
```bash
# Consumer timeout period when the Kafka consumer groups are used. If the broker does not receive the heartbeat of the consumer within this period, the consumer will be considered to have failed and the broker will initiate the rebalancing process. Currently, this value must be configured in the broker between 6000 (value of group.min.session.timeout.ms) and 300000 (value of group.max.session.timeout.ms).
session.timeout.ms=10000

# Interval at which the consumer sends a heartbeat when the Kafka consumer groups are used. This value must be smaller than the session.timeout.ms value, and is recommended to be smaller than one third of it.
heartbeat.interval.ms=3000

# Maximum interval allowed for calling the poll again when the Kafka consumer groups are used. If poll is not called within this time period, the consumer will be considered to have failed and the broker will reinitiate rebalancing to assign the partitions to other consumers.
max.poll.interval.ms=300000
```

If a consumer subscribes to many topics, you can try reducing the topics to which the consumer group subscribes.
