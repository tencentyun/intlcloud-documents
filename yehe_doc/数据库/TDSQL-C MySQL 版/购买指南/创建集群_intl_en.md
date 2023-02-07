This document describes how to create a cluster in the TDSQL-C for MySQL console.

## Prerequisites
To make a purchase, you need to complete identity verification first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=8), complete the **Database Configuration** settings, and click **Next**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Compute Billing Mode</td>
<td>Monthly subscription, pay-as-you-go, and serverless billing modes are supported.</td></tr>
<tr>
<td>Region</td>
<td>Select a region for database deployment.</td></tr>
<tr>
<td>Source AZ</td>
<td>Select an AZ for deployment. Specific AZs in the selected region are shown on the actual purchase page.</td></tr>
<tr>
<td>Multi-AZ Deployment</td>
<td>Select whether to enable multi-AZ deployment. If you enable it, the replica AZ option will appear.</td></tr>
<tr>
<td>Replica AZ</td>
<td>It is disabled by default and can be selected after multi-AZ deployment is enabled.</td></tr>
<tr>
<td>Network</td>
<td><ul><li>For performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C instances only in the same <a href="https://www.tencentcloud.com/document/product/215">VPC</a> in the same region.<br><li>A subnet is a logical network space in a VPC. You can create subnets in different AZs in the same VPC, which communicate with each other over the private network by default. Even if you select a subnet in another AZ in the same region, the network latency will not be increased because the actual business connection adopts nearby access.</li></ul></td></tr>
<tr>
<td>Compatible Database</td>
<td>MySQL 5.7 and 8.0 are supported.</td></tr>
<tr>
<td>Compute Instance Quantity</td>
<td>A cluster can contain one read-write instance and one or more read-only instances. We recommend at least two instances to ensure high availability of the cluster. After the cluster is created, you can improve its read capability by adding more read-only instances.</td></tr>
<tr>
<td>Instance specification</td>
<td>For more information on calculating the instance specification and storage capacity, see <a href="https://intl.cloud.tencent.com/document/product/1098/48406">Product Pricing</a>.</td></tr>
<tr>
<td>Storage Billing Mode</td>
<td><ul><li>Pay-as-you-go billing is supported, which means you only pay for the storage you use per hour and don't need to purchase any storage space here.<br></li><li>Monthly subscription billing is supported, which means you need to purchase monthly subscribed storage space now (billed in the entirety regardless of whether it is used up).</li></ul></td></tr>
<tr>
<td>Auto-renewal</td>
<td>Auto-renew the device monthly upon expiration if my account has sufficient balance</td></tr>
</tbody></table>
>?
>- If your desired instance specification is sold out, you can click **Do you need it?**, and the pop-up window will display instances of the same specification in other AZs. If none of them meet your requirements, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/DQGQ445_7.png)
>- Monthly subscribed storage space can be purchased only after you select the monthly subscription billing mode.
>- For more information on how to select an appropriate billing mode for storage space, see [Selecting Billing Mode for Storage Space](https://intl.cloud.tencent.com/document/product/1098/47633).
2. Complete the **Basic Info** and **Advanced Configuration** settings, select the **Validity Period** and **Quantity**, confirm the fees, and click **Buy Now**.
 - **Basic Info**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Cluster Name</td>
<td>Name the cluster now or later with up to 60 letters, digits, hyphens, underscores, and dots.</td></tr>
</tr>
<tr>
<td>Admin Username</td>
<td>The default value is `root`.</td>
</tr>
<tr>
<td>Password</td>
<td>The password can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and symbols <code>~!@#$%^&amp;*_-+=|\(){}[]:;'&lt;&gt;,.?/</code>.</td>
</tr>
<tr>
<td>Default Character Set</td>
<td>UTF8, GBK, LATIN1, and UTF8MB4 are supported.</td>
</tr>
<tr>
<td>Custom Port</td>
<td>It is 3306 by default and can be customized.</td>
</tr>
</tbody></table>
 - **Advanced Configuration**
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Security Group</td>
<td>Select or create a security group.</td></tr>
<tr>
<td>Parameter Template</td>
<td>Select or create a parameter template.</td></tr>
<tr>
<td>Table Name Case Sensitivity</td>
<td>Select **Case-Insensitive** or **Case-Sensitive**.</td></tr>
<tr>
<td>Project</td>
<td>Specify a project for the cluster to be created.</td></tr>
<tr>
<td>Alarm Policy</td>
<td>Select or create an alarm policy.</td></tr>
<tr>
<td>Tag</td>
<td>Add a tag to facilitate resource categorization and management.</td></tr>
<tr>
<td>Terms and Conditions</td>
<td>Read and indicate your consent to the terms and conditions.</td></tr>
</tbody></table>
>?
>- When you hover over **Configuration Fees**, the details such as computing fees and storage fees will be displayed.
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/fCiX357_8.png)
>- Cluster quantity
>Pay-as-you-go: You can purchase up to ten TDSQL-C for MySQL clusters in each AZ. If you need more, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>Monthly subscription: You can purchase an unlimited number of clusters.
>- When the amount of data stored in a cluster exceeds its maximum storage space, the cluster can only read but not write data. In this case, you can choose to delete redundant data or upgrade the specification.
>
3. After the purchase is completed, you will be redirected to the cluster list. After the status of the cluster becomes **Running**, it can be used normally.

## Subsequent operations
After creating the TDSQL-C for MySQL cluster, you can connect to it through its private or public network address or DMC. For more information, see [Connecting to Cluster](https://www.tencentcloud.com/document/product/1098/51980).
