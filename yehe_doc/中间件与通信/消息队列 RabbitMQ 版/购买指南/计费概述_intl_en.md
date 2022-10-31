
TDMQ for RabbitMQ is available in forms of exclusive cluster and virtual cluster:

- Exclusive cluster has been launched and made available commercially.
- Virtual cluster is currently in beta test free of charge and will stop service on January 1, 2023. You can migrate to exclusive cluster then. If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

This document describes the billing mode and billable items of TDMQ for RabbitMQ exclusive cluster.


## Billing Mode

 TDMQ for RabbitMQ exclusive cluster adopts the **monthly subscription** billing mode.


### Monthly subscription

Monthly subscription is a prepaid billing mode where you **pay first and then use the service**. When you purchase an exclusive cluster, the system will calculate the fees based on the cluster specification and purchase duration you select. You need to pay the fees before you can use the cluster. This billing mode is suitable for the long-term service with a relatively stable business traffic peak.



## Billable Items

TDMQ for RabbitMQ exclusive cluster fees are calculated as follows:

Cluster price = computing configuration price + storage configuration price = node unit price * number of nodes + storage unit price * storage size.

| Billable Item | Description |
| -------- | ------------------------------------------------------------ |
| Computing configuration | It refers to the computing service fees. Various node specifications are provided on demand. The price of a single node with each specification is fixed, and there are restrictions on the numbers of minimum and maximum nodes. The computing configuration price changes linearly based on the number of nodes. |
| Storage configuration | It refers to the storage service fees. You can customize the storage space in increments of 100 GB. The storage configuration price changes linearly based on the storage size. |



## Price Description

The specific price is as displayed on the [purchase page](https://buy.tencentcloud.com/tdmq?protocol=AMQP&rid=1&clusterType=profession). This section describes the performance differences between exclusive cluster specifications.



### Computing configuration

Computing configuration fees = node price * number of nodes

Cluster performance description: The **cluster performance is equal to node performance * number of nodes** and changes linearly within the node range.

> ?
>
> - The performance of the following specification is a reference value. The actual performance won't be any worse given the data measured during stress tests. Unexpected elastic capacity outside the specification won't cost anything either.
> - If the number of nodes in current specifications cannot meet your business requirements, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



| **Specification Type** | Single-Node Specification | **Minimum Nodes** | **Maximum Nodes** | **Single-Node Starting QPS (4 KB Message Size)** |
| ------------ | -------------------------------------------------- | -------------------- | -------------------- | -------------------------------- |
| Basic       | 2,000 QPS<br/>15 MB/s<br/>100 queues<br/>2,000 connections    | 1                    | 7 (odd only)          | 2,000                             |
| Standard       | 4,000 QPS<br/>30 MB/s<br/>200 queues<br/>3,000 connections    | 1                    | 7 (odd only)          | 5,000                             |
| Advanced I      | 8,000 QPS<br/>75 MB/s<br/>400 queues<br/>5,000 connections    | 1                    | 7 (odd only)          | 10,000                            |
| Advanced II     | 16,000 QPS<br/>150 MB/s<br/>800 queues <br/>8,000 connections | 1                    | 7 (odd only)          | 18,000                            |



TPS calculation rule

- Messaging TPS refers to the maximum sum of messages sent and subscribed per second.
- The message size is measured in 4 KB. For example, if the numbers of messages sent and received per second are both 10,000, and the average message body size is 16 KB, then the messaging TPS is (16 / 4) * (10,000 + 10,000) = 80,000 messages/sec.



### Storage configuration

Storage fees = storage space * storage unit price.

Each exclusive cluster version provides a minimum storage of 200 GB for a single node. You can choose a higher storage space in increments of 100 GB based on your business needs.

