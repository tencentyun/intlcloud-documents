## Overview

Cluster is a resource dimension in TDMQ for RocketMQ, and namespaces, topics, and groups of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of topics and message retention period. It is common for the development, test, and production environments to use their respective exclusive clusters.

Clusters are divided into virtual clusters and exclusive clusters:

- **Exclusive cluster**: Physical resources are exclusive, and data is secure. There are almost no use limits.
- **Virtual cluster**: Virtual computing and storage resources are used and automatically allocated based on usage. There are certain use limits.

**TDMQ for RocketMQ resource hierarchy**
![](https://qcloudimg.tencent-cloud.cn/raw/c613209d6cb2f4e924dfe15df85513c5.png)

## Directions

### Creating a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq) and enter the **Cluster** page.
2. On the **Cluster** page, select the region and click **Create Cluster** to enter the **Create Cluster** window.
  - Cluster Type: Select **Exclusive cluster** or **Virtual cluster**.
    - **Exclusive cluster**: Physical resources are exclusive, and data is secure. There are almost no use limits.
    - **Virtual cluster**: Virtual computing and storage resources are used and automatically allocated based on usage. There are certain use limits.
  - Billing Mode: Exclusive clusters are **monthly subscribed**, while virtual clusters are **pay-as-you-go**.
  - Region: Select a region closest to your business. Tencent Cloud products in different regions cannot communicate with each other over the private network. For example, CVM instances in Guangzhou region cannot access clusters in Shanghai region over the private network. Select a region with caution, as it cannot be changed after purchase. If you need cross-region communication over the private network, see [Creating Intra-account Peering Connection](https://intl.cloud.tencent.com/document/product/553/18836).
  - Cluster Specification: Select an appropriate cluster specification as needed.
  - Network Configuration: Public network access is not enabled by default. To enable it, [submit a ticket](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Fworkorder%2Fcategory%3Flevel1_id%3D876%26level2_id%3D1772%26source%3D0%26data_title%3D%25E6%25B6%2588%25E6%2581%25AF%25E9%2598%259F%25E5%2588%2597%2520TDMQ%26step%3D1) for application.
  - Cluster Name: Enter the cluster name, which can contain 3–64 digits, letters, hyphens, and underscores.
  - Tag: Tags are used to manage resources by category in different dimensions. For detailed directions, see [Managing Resource with Tag](https://intl.cloud.tencent.com/document/product/1113/43129).
3. Click **Buy Now**.

Next steps:

1. Create a namespace in the cluster and get the access address and connection information of the server. For more information, see [Namespace Management](https://intl.cloud.tencent.com/document/product/1113/43123)
2. Create a role in the cluster and grant it the production/consumption permissions of the namespace. For more information, see [Role and Authentication](https://intl.cloud.tencent.com/document/product/1113/43126)
3. Create a topic in the namespace as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1113/43124).
4. Write a demo as instructed in the [SDK documentation](https://www.tencentcloud.com/document/product/1113/45953) and configure the connection information for message production/consumption.

### Viewing cluster details

On the **Cluster** list page, click **View Details** in the **Operation** column to enter the cluster details page, where you can query the following information:

- Cluster overview (numbers of topics, messages produced in the last 24 hours, and currently retained messages)
- Cluster's basic information (cluster name/ID, region, creation time, and remarks)
- Cluster configuration:
  <table>
  <thead>
  <tr>
  <th>Instance Configuration</th>
  <th>Configuration Description</th>
  </tr>
  </thead>
  <tbody><tr>
  <td>Max TPS Per Topic Partition</td>
  <td>The upper limit for production TPS does not apply to consumption TPS.</td>
  </tr>
  <tr>
  <td>Max Namespaces</td>
  <td>Maximum number of namespaces that can be created.</td>
  </tr>
  <tr>
  <td>Max Topics</td>
  <td>Maximum number of topics that can be created.</td>
  </tr>
  <tr>
  <td>Max Groups</td>
  <td>Maximum number of groups that can be created.</td>
  </tr>
  <tr>
  <td>Message Retention Period</td>
  <td>Maximum message retention period that can be configured.</td>
  </tr>
  <tr>
  <td>Max Message Delay</td>
  <td>Maximum message consumption time delay.</td>
  </tr>
  </tbody></table>
  

![](https://qcloudimg.tencent-cloud.cn/raw/950f9b3f350dcac7e99ca09af85f295d.png)

### Getting the access address

On August 8, 2022, TDMQ for RocketMQ launched the virtual cluster feature in certain regions. The access addresses of new virtual clusters can be obtained in the namespace list. The access addresses of clusters created previously or not upgraded can still be obtained in **Access Address** in the **Operation** column.

- Clusters on the new version:
![](https://qcloudimg.tencent-cloud.cn/raw/91e590fce98e38121b3efa7243864128.png)
- Clusters on the old version:
![](https://qcloudimg.tencent-cloud.cn/raw/73da10eea086f8d28c77409e2b323407.png)

### Upgrading the cluster specification

If the current cluster specifications cannot meet your business needs, you can increase the number of nodes in the console.

> ?Currently, you can only increase the number of nodes but cannot modify the node or storage specification (which will be supported on the next version).

1. On the **Cluster** list page, click **Upgrade Configuration** in the **Operation** column.
2. Modify the number of nodes and click **Confirm Adjustment**.
    ![](https://qcloudimg.tencent-cloud.cn/raw/d5fb531836f8c35b845dac6073d21e67.png)


### Editing a cluster

1. On the **Cluster** list page, click **Edit** in the **Operation** column of the target cluster.
2. Enter the cluster name and remarks in the pop-up window and click **Submit**.

### Deleting a cluster

You can delete a created cluster in the following steps:

1. On the **Cluster** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.

> !After a cluster is deleted, all the configurations under it will be cleared and cannot be recovered. Therefore, caution should be exercised with this operation.

