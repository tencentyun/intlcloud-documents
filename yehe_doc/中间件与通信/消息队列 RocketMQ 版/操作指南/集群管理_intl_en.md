## Overview

Cluster is a resource dimension in TDMQ for RocketMQ, and namespaces, topics, and groups of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of topics and message retention period. It is common for the development, test, and production environments to use their respective dedicated clusters.

**TDMQ for RocketMQ resource hierarchy**
![](https://main.qcloudimg.com/raw/a98447d277622f79a33a9e5376d4ea95.png)

## Directions

### Creating cluster

1. Log in to the [TDMQ for RabbitMQ console](https://console.cloud.tencent.com/tdmq) and enter the **Cluster Management** page.
2. On the **Cluster Management** page, select the region and click **Create** to enter the **Create Cluster** window.
3. In the **Create Cluster** window, set the cluster attributes:
   ![](https://main.qcloudimg.com/raw/499c8c39bf37f1b39985e09d6ac6ee21.png)
   - Cluster Name: enter the cluster name, which can contain 3–64 letters, digits, hyphens, and underscores.
   - Remarks: enter the cluster remarks of up to 128 characters.
4. Click **OK**.
> !
> - Up to 5 virtual clusters can be created in one region.
> - No resource usage fees are charged during the beta test.

Next steps:

1. Get the access address (connection information of the server).
2. Create a [namespace](https://intl.cloud.tencent.com/document/product/1113/43123) in the cluster. 
3. Create a [role](https://intl.cloud.tencent.com/document/product/1113/43126) in the cluster and grant it the production/consumption permissions of the namespace.
4. Create a [topic](https://intl.cloud.tencent.com/document/product/1113/43124) in the namespace. 
5. Write a demo as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/1113/43132) and configure the connection information for message production/consumption.

### Viewing cluster details

On the **Cluster Management** list page, click **View Details** in the **Operation** column to enter the cluster details page.

On the details page, you can query:

- Cluster overview (numbers of topics, messages produced in the last 24 hours, and currently retained messages)
- Cluster's basic information (cluster name/ID, region, creation time, and remarks)
- Cluster configuration:

| Cluster Configuration | Description |
| ----------------- | ------------------------------------------------------------ |
| Maximum TPS per namespace |  Maximum TPS of one namespace (production TPS + consumption TPS). If this value is exceeded, requests will be throttled |
| Maximum number of namespaces | Maximum number of namespaces that can be created                                     |
| Maximum number of topics                | Maximum number of topics that can be created                                       |
| Maximum number of groups | Maximum number of groups that can be created |
| Message retention period                  | Maximum message retention period that can be configured. A shorter period can be configured at the namespace level |
| Maximum message delay | Maximum time of delayed message consumption |

![](https://main.qcloudimg.com/raw/35d27c2873af355df373c6d389bf9888.png)

### Getting access address

On the **Cluster Management** list page, click **Access Address** in the **Operation** column to get the access address of the cluster.

![](https://main.qcloudimg.com/raw/4fed5e6a2497995613b645f6a9a7e206.png)

### Editing cluster

1. On the **Cluster Management** list page, click **Edit** in the **Operation** column of the target cluster.
2. Enter the cluster name and remarks in the pop-up window and click **Submit**.

### Deleting cluster

You can delete a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.

>!After a cluster is deleted, all the configurations under it will be cleared and cannot be recovered. Therefore, caution should be exercised with this operation.
