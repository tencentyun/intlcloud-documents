## Overview

Cluster is a resource dimension in TDMQ for RabbitMQ, and vhosts, exchanges, and queues of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of exchanges and message retention period. It is common for the development, test, and production environments to use their respective dedicated clusters.

**TDMQ for RabbitMQ resource hierarchy**

![](https://qcloudimg.tencent-cloud.cn/raw/2ce6bd44187b5e06d67b4d74264bb832.svg)

## Directions

### Creating cluster

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq) and enter the **Cluster Management** page.
2. On the **Cluster Management** page, select the region and click **Create Cluster** to enter the **Create Cluster** window.
3. In the **Create Cluster** window, set the cluster attributes:
  ![](https://qcloudimg.tencent-cloud.cn/raw/733658dcc12580739963b8bccb0aafd1.png)
   - Cluster Name: enter the cluster name, which can contain 3–64 letters, digits, hyphens, and underscores.
   - Cluster Remarks: enter the cluster remarks.
4. Click **OK**.
> !
> - Up to 5 clusters can be created in one region.
> - No resource usage fees are charged during the beta test.

Next steps:

1. Get the access address (connection information of the server).
2. Create a [vhost](https://intl.cloud.tencent.com/document/product/1112/43073) in the cluster and get the username and password. 
3. Create an [exchange](https://intl.cloud.tencent.com/document/product/1112/43074) and [queue](https://intl.cloud.tencent.com/document/product/1112/43075) in the vhost.
4. Create a [binding](https://intl.cloud.tencent.com/document/product/1112/43076) between the exchange and queue. 
5. Write a demo and configure the connection information for message production/consumption.

### Viewing cluster details

On the **Cluster Management** list page, click the ID of the target cluster to enter the cluster details page.

On the details page, you can query:

- Cluster overview (numbers of queues, messages produced in the last 24 hours, and currently retained messages)
- Cluster's basic information (cluster name/ID, region, access address, creation time, and remarks)
- Cluster configuration:

| Cluster Configuration | Description |
| --------------------------- | ------------------------------------------------------------ |
| Maximum TPS per vhost                      |  Maximum TPS of one vhost (production TPS + consumption TPS). If this value is exceeded, requests will be throttled |
| Maximum number of client connections per vhost | Maximum number of clients that can be connected to one vhost       |
| Maximum number of vhosts | Maximum number of vhosts that can be created in one cluster |
| Maximum number of exchanges | Maximum number of exchanges that can be created in one cluster |
| Maximum number of queues | Maximum number of queues that can be created in one cluster |
| Message retention period | Maximum message retention period that can be configured. A shorter period can be configured at the vhost level |

![](https://qcloudimg.tencent-cloud.cn/raw/ff55127e7f34efa5591a2e10ccc40f85.png)

### Getting access address

On the **Cluster Management** list page, click **Access Address** in the **Operation** column to get the access address of the cluster.

![](https://qcloudimg.tencent-cloud.cn/raw/75e6f78d3b841c02432bec9d9e8cb7c5.png)

### Editing cluster

You can edit a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Edit** in the **Operation** column of the target cluster.
2. Enter the cluster name and remarks in the pop-up window and click **Submit**.

### Deleting cluster

You can delete a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.

> !After a cluster is deleted, all the configurations under it will be cleared and cannot be recovered. Therefore, caution should be exercised with this operation.
