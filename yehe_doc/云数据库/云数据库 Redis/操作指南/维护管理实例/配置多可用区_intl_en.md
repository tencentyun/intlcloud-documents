This document describes how to configure multiple availability zones for your TencentDB for Redis instance and how to view them in the console.

## Overview
You can deploy TencentDB for Redis master node and replica nodes in different availability zones of the same region. [Multi-AZ deployed instances](https://intl.cloud.tencent.com/document/product/239/39812) have higher availability and better disaster recovery capability than single-AZ deployed instances.
- Read/write separation disabled (that is, replicas can be written to and read from): write/read requests in a replica availability zone are routed by proxy to the master node, and the master node synchronizes with replica nodes to ensure consistent data across all nodes. In this process, only one cross-AZ access happens.
- Read/write separation enabled (that is, replicas can only be read from): write requests are routed by proxy to the master node, but read requests in a replica availability zone are routed to the replica node in the same replica availability zone so that read requests can get responded by the nearest node.

We recommend you deploy one master node and one replica node in the master availability zone, and another replica node in the replica availability zone. If the master node fails, the replica node in the master availability zone can be promoted quickly to avoid cross-AZ master-replica switch. Such a deployment solution can maximize service availability and reduce the delay caused by master node failures.

>?Currently, TencentDB for Redis 4.0 and 5.0 instances in standard or cluster architecture support multi-AZ deployment.


## Directions
### Enabling multi-AZ deployment
1. Log in to the [Redis Purchase Page](https://buy.cloud.tencent.com/redis), specify instance information including region, availability zones, and replicas, and click **Buy Now**.
 - Replica count: the maximum number of availability zones = the number of replicas + 1.
 - Availability zone: deploy Redis nodes in different availability zones. Up to six availability zones are supported.
![](https://main.qcloudimg.com/raw/d76a6c8cc996b58c8f5df1a17102111c.png)
2. After the purchase is completed, you will be redirected to the instance list. After the status of the instance changes to **Running**, it can be used normally.

### Viewing multi-AZ deployment details
- Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis). In the **Availability Zone** column in the instance list, the **M** tag indicates that nodes of this instance are deployed in multiple availability zones. Mouse over the tag to view details.
![](https://main.qcloudimg.com/raw/5c553bf4c0817c0dbddb662405078fe7.png)
- In the [instance list](https://console.cloud.tencent.com/redis), click an instance ID/name and enter the instance management page. In the **Basic Info** section on the **Instance Details** tab, the **M** tag next to **Availability Zone** indicates that nodes of this instance are deployed in multiple availability zones. Mouse over the tag to view details.
![](https://main.qcloudimg.com/raw/d579e1ab309c754ef0ea56904ad5f194.png)
- In the [instance list](https://console.cloud.tencent.com/redis), click an instance ID/name and enter the instance management page. On the **Manage Node** tab, you can view node details and adjust node configurations.
![](https://main.qcloudimg.com/raw/aa0adb39b9bfb543051ca6bdfda78664.png)
