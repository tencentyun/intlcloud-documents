TDMQ for RocketMQ is available in forms of exclusive cluster and virtual cluster:

- Virtual cluster is currently in beta test free of charge through November 2022 and will be commercially launched then. The specific beta test end time and pricing information will be sent to you in advance by SMS, Message Center, or announcements in the console.
- Exclusive cluster has been launched and made available commercially. 

This document describes the billing mode and billable items of TDMQ for RocketMQ exclusive cluster.

## Billing Mode

 TDMQ for RocketMQ exclusive cluster adopts the **monthly subscription** billing mode.

#### Monthly subscription

Monthly subscription is a prepaid billing mode where you **pay first and then use the service**. When you purchase an exclusive cluster, the system will calculate the fees based on the cluster specification and purchase duration you select. You need to pay the fees before you can use the cluster. This billing mode is suitable for the long-term service with a relatively stable business traffic peak.



## Billable Items

TDMQ for RocketMQ exclusive cluster fees are calculated as follows:

Cluster price = minimum configuration price + computing configuration price + storage configuration price = minimum configuration price + node unit price * number of nodes + storage unit price * storage size.

| Billable Item | Description |
| -------- | ------------------------------------------------------------ |
| Minimum configuration | It refers to the fixed fees of a new cluster for basic services such as cluster management, message management, observability, and high availability, which will not increase as the cluster size increases. |
| Computing configuration | It refers to the computing service fees. Various node specifications are provided on demand. The price of a single node with each specification is fixed, and there are restrictions on the numbers of minimum and maximum nodes. The computing configuration price changes linearly based on the number of nodes. |
| Storage configuration | It refers to the storage service fees. You can customize the storage space in increments of 100 GB. The storage configuration price changes linearly based on the storage size. |





## Price Description

The specific price is as displayed on the [purchase page](https://buy.tencentcloud.com/tdmq?protocol=RocketMQ&rid=1&clusterType=profession). This section describes the performance differences between exclusive cluster specifications.

> ?If the number of nodes in current specifications cannot meet your business requirements, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



### Minimum configuration

The performance of the following specification is a reference value. The actual performance won't be any worse given the data measured during stress tests. Unexpected elastic capacity outside the specification won't cost anything either.

| Specification Type | Single-Node Specification                     |
| -------- | ------------------------------ |
| Basic   | 2,000 QPS<br>40 MB/s<br>4,000 topic partitions    |
| Standard   | 5,000 QPS<br>80 MB/s<br>8,000 topic partitions    |
| Advanced I  | 10,000 QPS<br>150 MB/s<br>10,000 topic partitions |
| Advanced II | 18,000 QPS<br>300 MB/s<br>12,000 topic partitions |





### Computing configuration

Computing configuration fees = node price * number of nodes

Cluster performance description: The <b>cluster performance is equal to node performance * number of nodes</b> and changes linearly within the node range.

| **Specification Type** | **Minimum Nodes** | **Maximum Nodes** | **Single-Node Starting QPS (4 KB Message Size)** |
| ------------ | -------------------- | -------------------- | -------------------------------- |
| Basic        | 2                    | 10                   | 2,000                             |
| Standard       | 2                    | 10                   | 5,000                             |
| Advanced I      | 2                    | 20                   | 10,000                            |
| Advanced II     | 2                    | 20                   | 18,000                            |

TPS calculation rule

- Messaging TPS refers to the maximum sum of messages sent and subscribed per second.
- The message size is measured in 4 KB. For example, if the numbers of messages sent and received per second are both 10,000, and the average message body size is 16 KB, then the messaging TPS is (16 / 4) * (10,000 + 10,000) = 80,000 messages/sec.



### Storage configuration

Storage fees = storage space * storage unit price.

Each exclusive cluster version provides a minimum storage of 200 GB for a single node. You can choose a higher storage space in increments of 100 GB based on your business needs.
