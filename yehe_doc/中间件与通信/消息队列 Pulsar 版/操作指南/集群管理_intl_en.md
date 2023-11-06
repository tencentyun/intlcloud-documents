## Overview

Cluster is a resource dimension in TDMQ for Pulsar, and namespaces, topics, and role permissions of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of topics and message retention period. It is common for the development, test, and production environments to use their respective dedicated clusters.

Clusters are divided into virtual clusters and professional clusters:

- **Virtual cluster**: Virtual computing and storage resources are used and automatically allocated based on usage. There are certain use limits. You don't need to pay for resources, and you can create up to 5 virtual clusters under each account.
- **Professional cluster**: Physical resources are exclusive, and data is secure. There are almost no use limits. Resource usage fees will be charged even if resources are idle.

> ?
>
> - Professional cluster resources are unavailable currently. They can be applied for after the product is commercially launched. You will be notified by email and SMS one month in advance.
> - Currently, clusters are available in multiple versions. For more information, see [Cluster Version Updates](https://intl.cloud.tencent.com/document/product/1110/42898).

**TDMQ for Pulsar resource hierarchy**
![](https://qcloudimg.tencent-cloud.cn/raw/af334efc11f390763e0b979a7e90acd3.png)


## Directions

### Creating a cluster

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and enter the **Cluster Management** page.
2. On the **Cluster Management** page, select the region and click **Create Cluster** to enter the **Create Cluster** window.
3. In the **Create Cluster** window, select the cluster type and set the cluster attributes:
   - Cluster Name: Set the name of the environment, which can contain up to 64 digits, letters, and special symbols (-\_=:.).
   - Public Network Access: It is not enabled by default. To enable it, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=1772&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20TDMQ&step=1) for application. We recommend you only enable this option for development and test clusters as it cannot be disabled once enabled.
   - Cluster Description: Enter the cluster description of up to 128 characters.
   - Resource Tag: Set a resource tag. For more information, see [Managing Resource with Tag](https://intl.cloud.tencent.com/document/product/1110/42939).
4. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/04ebb189460de4b51f7a24d815d5dca7.png)

> ? Each user can create up to 5 virtual clusters.

#### Subsequent steps

1. [Get the access address](#Getting-access-address) to get the connection information of the server (only clusters on v2.6.1 require configuring an access point; for clusters on v2.7.1 or later, the access address can be copied directly).
2. Create a namespace as instructed in [Namespace](https://intl.cloud.tencent.com/document/product/1110/42929) in the cluster. 
3. Create a role as instructed in [Role and Authentication](https://intl.cloud.tencent.com/document/product/1110/42936) in the cluster and grant it the production/consumption permissions of the namespace.
4. Create a topic as instructed in [Topic Management](https://intl.cloud.tencent.com/document/product/1110/42930) in the namespace. 
5. Write a demo as instructed in [SDK Overview](https://intl.cloud.tencent.com/document/product/1110/42945) and configure the connection information and token for message production/consumption.



### Viewing cluster details

On the **Cluster Management** list page, click the ID of the target cluster to enter the cluster details page, where you can view the following information:
- Cluster Statistics: This section displays the average message size, production speed, and consumption speed, the number of produced messages, and the accumulative storage duration in the selected time range.
>? The statistics feature is not supported for clusters on v2.6.x.
<table>
<tr>
<th>Metric</th>
<th>Description</th>
</tr>
<tr>
<td>Avg Message Size</td>
<td>Average size of message data (including message headers and bodies) in the selected time range.</td>
</tr>
<tr>
<td>Avg Production Speed</td>
<td>Average number of messages produced to the cluster per second in the selected time range.</td>
</tr>
<tr>
<td>Avg Consumption Speed</td>
<td>Average number of messages the cluster pushes to the client per second in the selected time range.</td>
</tr>
<tr>
<td>Produced Messages</td>
<td>The number of messages produced to the cluster in the selected time range.</td>
</tr>
<tr>
<td>Storage Duration</td>
<td>Total storage space used by message data as of the last time point of the selected time range (it changes only when the last time point changes).</td>
</tr>
</table>
- Cluster's basic information: Cluster name/ID, version, access address (available for clusters on v2.7.1 or later only), region, creation time, and description.
- Cluster configuration:
![](https://qcloudimg.tencent-cloud.cn/raw/d555d9c26bb6bd5dd573e7451945ef81.png)
<table>
<tr>
<th>Cluster Configuration</th>
<th>Configuration Description</th>
</tr>
<tr>
<td>Max Production TPS Per Namespace</td>
<td>Maximum production TPS per namespace. If this value is exceeded, requests will be throttled.</td>
</tr>
<tr>
<td>Max Consumption TPS Per Namespace</td>
<td>Maximum consumption TPS per namespace. If this value is exceeded, requests will be throttled.</td>
</tr>
<tr>
<td>Max Production Bandwidth Per Namespace</td>
<td>Maximum production bandwidth per namespace.</td>
</tr>
<tr>
<td>Max Consumption Bandwidth Per Namespace</td>
<td>Maximum consumption bandwidth per namespace.</td>
</tr>
<tr>
<td>Max Namespaces</td>
<td>Maximum number of namespaces that can be created per cluster.</td>
</tr>
<tr>
<td>Max Topics</td>
<td>Maximum number of topics that can be created per namespace.</td>
</tr>
<tr>
<td>Message Retention Period</td>
<td>Maximum message retention period that can be configured. A shorter period can be configured at the namespace level.</td>
</tr>
<tr>
<td>Max Message Storage	</td>
<td>Maximum disk capacity used by message heap. After this value is exceeded, new messages cannot be produced (under normal circumstances, there should not be too many retained messages; if this is not the case, check whether the business is consuming messages normally).</td>
</tr>
<tr>
<td>Max Message Delay	</td>
<td>Maximum message consumption time delay.</td>
</tr>
</table>



### Getting the access address[](id:Getting-access-address)

On the **Cluster Management** list page, click **Access Address** in the **Operation** column of the target cluster. You can get the access address in the following ways:

<dx-tabs>
::: Clusters on v2.7.1 or later
You can directly get the access address as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/4ee11d11a3a2f36c953c2c4e4667777f.png)
:::
::: Clusters on v2.6.1
On the access point list page, click **Create** and enter the access point information to configure the access point.

- VPC: Select the VPC in which you want to deploy your client.
- Subnet: Select any subnet in the VPC.
- Enter the remarks.



<dx-alert infotype="explain" title="">
A cluster can be configured with multiple access points. Currently, only VPC access is supported.
</dx-alert>
:::

</dx-tabs>

### Deleting a cluster

You can delete a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.
