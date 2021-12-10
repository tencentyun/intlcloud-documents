## Overview

Cluster is a resource dimension in TDMQ for Pulsar, and namespaces, topics, and role permissions of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of topics and message retention period. It is common for the development, test, and production environments to use their respective dedicated clusters.

Clusters are divided into virtual clusters and dedicated clusters:

- **Virtual cluster**
  Virtual computing and storage resources are used and automatically allocated based on usage. There are certain use limits. You don't need to pay for resources, and you can create up to 5 virtual clusters under each account.
- **Dedicated cluster**
  Physical resources are exclusive, and data is secure. There are almost no use limits. Resource usage fees will be charged even if resources are idle.

> ?
> - Dedicated cluster resources are unavailable during the beta test. They can be applied for after the product is commercially launched. You will be notified by email and SMS one month in advance.
> - Currently, clusters are available in multiple versions. For more information, see [Cluster Version Release Notes](https://intl.cloud.tencent.com/document/product/1110/42898).

**TDMQ for Pulsar resource hierarchy**
![](https://qcloudimg.tencent-cloud.cn/raw/af334efc11f390763e0b979a7e90acd3.png)



## Directions

### Creating cluster

1. Log in to the [TDMQ for Pulsar console](https://console.cloud.tencent.com/tdmq) and enter the **Cluster Management** page.
2. On the **Cluster Management** page, select the region and click **Create Cluster** to enter the **Create Cluster** window.
3. In the **Create Cluster** window, select the cluster type and set the cluster attributes:
   - Cluster Name: enter the cluster name, which cannot be modified after creation and can contain up to 64 letters, digits, hyphens, and underscores.
   - Remarks: enter the cluster remarks of up to 200 characters.
4. Click **OK**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/f689b91b002442c37cb6fa3e1f9cc5c1.png)

> ?
> - Each user can create up to 5 virtual clusters.
> - No resource usage fees are charged during the beta test.

Next steps:

1. [Get the access address](#Getting-access-address) to get the connection information of the server (only clusters on v2.6.1 require configuring an access point; for clusters on v2.7.1 or above, the access address can be copied directly).
2. Create a [namespace](https://intl.cloud.tencent.com/document/product/1110/42929) in the cluster. 
3. Create a [role](https://intl.cloud.tencent.com/document/product/1110/42936) in the cluster and grant it the production/consumption permissions of the namespace.
4. Create a [topic](https://intl.cloud.tencent.com/document/product/1110/42930) in the namespace. 
5. Write a demo as instructed in the [SDK documentation](https://intl.cloud.tencent.com/document/product/1110/42945) and configure the connection information and token for message production/consumption.



### Viewing cluster details

On the **Cluster Management** list page, click the ID of the target cluster to enter the cluster details page.

On the details page, you can query:

- Cluster's basic information: cluster name/ID, version, access address (available for clusters on v2.7.1 or above only), region, creation time, and remarks.
- Cluster configuration:

| Cluster Configuration Item                      | Description                                                     |
| ----------------------------- | ------------------------------------------------------------ |
| Maximum QPS                      |  Maximum QPS of the cluster (production QPS + consumption QPS). If this value is exceeded, requests will be throttled |
| <nobr>Maximum number of namespaces</nobr> | Maximum number of namespaces that can be created                                     |
| Maximum number of topics                | Maximum number of topics that can be created                                       |
| Message retention period                  | Maximum message retention period that can be configured. A shorter period can be configured at the namespace level |
| Maximum storage capacity                  | Maximum disk capacity used by message retention. After this value is exceeded, new messages cannot be produced (under normal circumstances, there should not be too many retained messages; if this is not the case, check whether the business is consuming messages normally) |

![](https://qcloudimg.tencent-cloud.cn/raw/4c16ad325eb626387bf35e836af7fbe6.png)



### Getting access address[](id:Getting-access-address)

On the **Cluster Management** list page, click **Access Address** in the **Operation** column of the target cluster. You can get the access address in the following ways:

<dx-tabs>
::: Clusters\son\sv2.7.1\sor\sabove
You can directly get the access address as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/611474fd348337c008d5b8ef6630d44b.png)
:::
::: Clusters\son\sv2.6.1
On the access point list page, click **Create** and enter the access point information to configure the access point.

- VPC: select the VPC in which you want to deploy your client.
- Subnet: select any subnet in the VPC.
- Enter the remarks.



<dx-alert infotype="explain" title="">
A cluster can be configured with multiple access points. Currently, only VPC access is supported.
</dx-alert>
:::

</dx-tabs>

### Deleting cluster

You can delete a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.
