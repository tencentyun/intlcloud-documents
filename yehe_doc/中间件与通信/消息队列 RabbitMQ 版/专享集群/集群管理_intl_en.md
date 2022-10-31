## Overview

Cluster is a resource dimension in TDMQ for RabbitMQ, and vhosts, exchanges, and queues of different clusters are completely isolated from each other. Each cluster has its own resource limits, such as the total number of exchanges and message retention period. It is common for the development, test, and production environments to use their respective dedicated clusters.

Clusters are divided into virtual clusters and exclusive clusters:

- **Virtual cluster**: Virtual computing and storage resources are used and automatically allocated based on usage. There are certain use limits. You can create up to 50 virtual clusters under each account.
- **Exclusive cluster**: Physical resources are exclusive, and data is secure. There are almost no use limits.

This document describes how to create, view, edit, and delete an exclusive cluster in the TDMQ for RabbitMQ console.



## Directions

### Creating a cluster

1. Log in to the [TDMQ console](https://console.cloud.tencent.com/tdmq).
2. Select **RabbitMQ** > **Cluster** on the left sidebar and click **Create Cluster** to enter the purchase page.
3. On the purchase page, select the target instance specification.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Cluster Type</td>
<td>Yes</td>
<td>Select <strong>Exclusive cluster</strong>.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Yes</td>
<td>TDMQ for RabbitMQ exclusive cluster adopts the <strong>monthly subscription</strong> billing mode.</td>
</tr>
<tr>
<td>Region</td>
<td>Yes</td>
<td>Select a region close to resources of the deployed client. <strong>Cloud products in different regions are not interconnected over private networks and the region cannot be changed after you purchase the service. Proceed with caution.</strong></td>
</tr>
<tr>
<td>AZ</td>
<td>Yes</td>
<td>Select an AZ as needed. Currently, only <strong>single-AZ deployment</strong> is supported.</td>
</tr>
<tr>
<td>Node Specification</td>
<td>Yes</td>
<td>Select an appropriate node specification based on your business needs.</td>
</tr>
<tr>
<td>Node Count</td>
<td>Yes</td>
<td>Select an appropriate number of nodes based on your business needs.</td>
</tr>
<tr>
<td>Single-Node Storage Specification</td>
<td>Yes</td>
<td>Message storage is billed separately, and messages can be retained without limit in the purchased storage capacity. The actual storage usage can be estimated by multiplying the message production traffic by the retention period.</td>
</tr>
<tr>
<td>Cluster Specification</td>
<td>No</td>
<td>The <strong>cluster performance is equal to node performance * number of nodes</strong> and changes linearly within the node range.</td>
</tr>
<tr>
<td>VPC</td>
<td>Yes</td>
<td>Bind the domain name of the new cluster's access point to the selected VPC.</td>
</tr>
<tr>
<td>Cluster Name</td>
<td>Yes</td>
<td>Enter the cluster name, which can contain 3–64 digits, letters, hyphens, and underscores.</td>
</tr>
<tr>
<td>Tag</td>
<td>No</td>
<td>Tags are used to categorize and manage resources. For more information, see <a href="https://intl.cloud.tencent.com/document/product/597/41600">Tag Overview</a>.</td>
</tr>
</tbody></table>
4. Select **I have read and agree to TDMQ for RabbitMQ Terms of Service** and click **Buy Now**.
5. On the order payment page, click **Pay** and wait 3–5 minutes. Then, you can see the created cluster on the **Cluster** page.




### Viewing cluster details

On the **Cluster Management** list page, click the ID of the target cluster to enter the cluster details page.

On the details page, you can query:

- Cluster's basic information: The cluster's name/ID, region, access address, creation time, and description.
- Network information: The cluster's VPC, public network access address, web console login address, username, and password.
- Cluster specification: The cluster's specification type, maximum TPS, peak bandwidth, and storage space.



### Getting the access address

On the **Cluster Management** list page, click **Access Address** in the **Operation** column to get the access address of the cluster.



### Editing a cluster

You can edit a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Edit** in the **Operation** column of the target cluster.
2. Enter the cluster name and remarks in the pop-up window and click **Submit**.

### Deleting a cluster

You can delete a created cluster in the following steps:

1. On the **Cluster Management** list page, click **Delete** in the **Operation** column of the target cluster.
2. In the deletion confirmation pop-up window, click **Delete**.

> ?After a cluster is deleted, all the configurations under it will be cleared and cannot be recovered. Therefore, caution should be exercised with this operation.
