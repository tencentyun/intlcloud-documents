Advanced monitoring supported in CKafka Pro allows you to view metrics such as core services, production, consumption, and broker GC in the console, making it easier for OPS personnel to troubleshoot issues.

This document describes how to view advanced monitoring metrics in the console and explains the meaning of advanced monitoring metrics.

## Monitoring Metric Description

### Core service monitoring

| Monitoring Metric | Description | Normal Value Range |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Network traffic level | Remaining IO resources for concurrent processing in the instance. The closer the value to 1, the more idle resources there are. | This value generally fluctuates between 0.5 and 1, and less than 0.3 means the load is high. |
| Request queue depth | Number of unprocessed production requests. A large value implies that there are too many concurrent requests, the CPU load is too high, or the disk IO hits a bottleneck. | If the value continuously stays at 2000, the cluster load is relatively high. It can be ignored when the value is less than 2000.|
| Number of unsynced replicas | Number of unsynced replicas in the cluster. When an instance has unsynced replicas, there may be a problem with the health of the cluster. | If the curve value is greater than 5 for a long time (because some of the built-in topic partitions of Tencent Cloud may be offline and have nothing to do with the business), you need to deal with the issue. Occasionally broker fluctuates and the value rises, but after a period of time, it returns to stability, which is normal. |
| Number of ZooKeeper disconnections | Number of times the persistent connection between broker and Zookeeper is disconnected and reconnected. Network fluctuations and high cluster load may cause disconnections and reconnections, which will lead to leader switch. | No normal value range. The number of ZooKeeper disconnections is a cumulative number. A larger number does not mean that there are problems with the cluster. This metric is for reference only. |
| Number of ISR expansions | Kafka ISR expansions occur when the data in unsynced replicas becomes consistent with the data in leader. In this case, the unsynced replicas will rejoin ISR, and the number of ISR expansions will increase by 1. | No normal value range. When the cluster fluctuates, ISR expansions happen. There is no need to pay attention if the value is greater than 0 only for a short time. |
| Number of ISR shrinks | Kafka ISR shrinks occur when a broker breaks down and reconnects to ZooKeeper. | No normal value range. When the cluster fluctuates, ISR shrinks happen. There is no need to pay attention if the value is greater than 0 only for a short time. |

### Production monitoring

| Monitoring Metric  | Description | Normal Value Range |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Total Production Time | Total time taken by the production request, which is the sum of request queue time, local processing time, response delay time, etc. <br/>At each time point, the total time is not equal to the accumulation of the time of following 5 metrics, because each metric indicates the average time. | Usually the value is between 0 ms and 100 ms. When the data volume is large, the normal range is between 0 ms to 1000 ms. It can be ignored as long as the value doesn’t remain greater than 1000 ms for a long time.|
| Request queue time | Time that the production request waits in the request queue for subsequent processing. | Usually the value is between 0 ms and 50 ms. When the data volume is large, the normal range is between 0 ms to 200 ms. It can be ignored as long as the value doesn’t remain greater than 200 ms for a long time. |
| Local processing time | Time that the production request is processed by the leader broker, that is, the time when the request packet is taken out of the request queue and written into the local page cache. | Usually the value is between 0 ms and 50 ms. When the data volume is large, the normal range is between 0 ms and 200 ms. It can be ignored as long as the value doesn’t remain greater than 200 ms for a long time. |
| ACK waiting time | Time that the production request is waiting for data synchronization. The value will be greater than 0 if the client ACK is -1, that is, if ACK is 1 or 0, the value is 0. | Usually the value is between 0 ms and 200 ms. When the data volume is large, the normal range is between 0 ms and 500 ms. It can be ignored as long as the value doesn’t remain greater than 500 ms for a long time. If ACK is -1, the value of a cross-AZ instance will be greater than that of a non-cross-AZ instance. |
| Response delay time | Time for which the response to the production request is delayed by the system. When the instance's traffic does not exceed the purchased traffic, the value is 0; otherwise, the value is greater than 0. | If the instance's traffic does not exceed the purchased traffic, the value is 0; otherwise, response will be delayed for 0 to 5 minutes depending on how much exceeds the purchased traffic. So the maximum value is 5 minutes. |
| Response queue time | Time that the production request waits in the response queue to be sent to the client. | Usually the value is between 0 ms and 50 ms. When the data volume is large, the normal range is between 0 ms and 200 ms. It can be ignored as long as the value doesn’t remain greater than 200 ms for a long time. |

### Consumption monitoring

| Monitoring Metric     |  Description  | Normal Value Range |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Total consumption time | Total time taken by the production request, which is the sum of request queue time, local processing time, etc. <br/>At each time point, the total time is not equal to the accumulation of the time of following 5 metrics, because each metric indicates the average time. | Generally the value is between 500 ms and 1000 ms (for the client, the default value of `fetch.max.wait.ms` is `500 ms`). When the data volume is large, a value between 500 ms and 5000 is normal. |
| Request queue time | Time that the consumption request waits in the request queue for subsequent processing. | Generally the value is between 0 ms and 50 ms. When the data volume is large, a value between 0 ms and 200 ms is normal. It can be ignored as long as the value doesn’t remain greater than 200 ms for a long time. |
| Local processing time | Time that the consumption request reads data from the leader broker (or local disk). | Generally the value is between 0 ms and 500 ms. When the data volume is large, a value between 0 ms to 1000 ms is normal. It can be ignored as long as the value doesn’t remain greater than 1000 ms for a long time, because sometimes cold data might be read during consumption, which takes extra time. |
| Consumption waiting time | Maximum amount of time the server will wait before answering the request from the client if the client cannot read any data. It is the value set in the `fetch.max.wait.ms` parameter on the client, which is `500ms` by default. | Generally the value is around 500 ms, but it depends on the parameter setting.|
| Response delay time | Time for which the response to the consumption request is delayed by the system. When the instance's traffic does not exceed the purchased traffic, the value is 0; otherwise, the value is greater than 0. | If instance's traffic does not exceed the purchased traffic, the value is 0; otherwise, response will be delayed for 0 to 5 minutes depending on how much exceeds the purchased traffic. So the maximum value is 5 minutes. |
| Response queue time | Time that the consumption request waits in the response queue to be sent to the client. | Usually the value is between 0 ms and 50 ms. When the data volume is large, a value between 0 ms and 200 ms is normal. It can be ignored as long as the value doesn’t remain greater than 200 ms for a long time. |

### Broker GC monitoring

| Monitoring Metric | Description | Normal Value Range |
| -------------- | -------------------- | ---------------------------------------------------- |
| Young GCs | Number of young GCs in brokers | Normally, the number is between 0 and 300. If the number continues being greater than 300, you need to adjust the GC parameters. |
| Old GCs | Number of old GCs in brokers | Normally, the number is 0. If the number is greater than 0, you need to deal with it.  |

## Viewing Monitoring Data

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. In the instance list, click the ID/name of an instance to go to the instance details page.
3. At the top of the instance details page, Click **Monitor** > **Advanced Monitoring**, select a metric tab, and set the time range to view the monitoring data.
