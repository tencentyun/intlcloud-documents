This document describes how to create a Serverless cluster in the TDSQL-C for MySQL console.

## Prerequisites
To make a purchase, you need to complete identity verification first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=8) and complete the **Database Configuration** settings.
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Database Engine</td>
<td>Select **MySQL**.</td></tr>
<tr>
<td>Compute Billing Mode</td>
<td>Select **Serverless**.</td></tr>
<tr>
<td>Region</td>
<td>Select a region for database deployment.<dx-alert infotype="explain" title="">
Currently, the Serverless billing mode is supported only in Guangzhou, Shanghai, Beijing, and Nanjing regions. If you need to use it in other regions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
</dx-alert></td></tr>
<tr>
<td>Source AZ</td>
<td>Select an AZ for deployment. Specific AZs in the selected region are shown on the actual purchase page.</td></tr>
<tr>
<td>Multi-AZ Deployment</td>
<td>Currently, Serverless instances don't support multi-AZ deployment.</td></tr>
<tr>
<td>Network</td>
<td>For performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C instances only in the same <a href="https://www.tencentcloud.com/document/product/215">VPC</a>.</td></tr>
<tr>
<td>Compatible Database</td>
<td>MySQL 5.7 and 8.0 are supported.</td></tr>
<tr>
<td>Compute Unit</td>
<td>Select the upper and lower limits of the compute unit (CCU), and the instance will be automatically and elastically scaled within the selected resource range.<dx-alert infotype="explain" title="">
CynosDB Compute Unit (CCU) is the computing and billing unit for the Serverless Edition. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater value between the number of CPU cores used by the database and 1/2 of the memory size. For more information, see [Compute Unit](https://www.tencentcloud.com/document/product/1098/51975).
</dx-alert></td></tr>
<tr>
<td>Auto-Pause</td>
<td>Configure the automatic pause time of the instance. If there is no connection to access the database within the set time, the instance will be automatically paused, with billing stopped.</td></tr>
<tr>
<td>Storage Billing Mode</td>
<td>The default storage billing mode of the Serverless instance is pay-as-you-go.</td></tr>
</tbody></table>
2. Select the number of instances. You can batch purchase multiple Serverless instances of the same specification. Then, click **Next**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/r2Tz089_1.png)
3. Complete the **Basic Info** and **Advanced Configuration** settings, confirm the fees, and click **Buy Now**.
 - **Basic Info**
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Cluster Name</td>
<td>Name the cluster now or later with up to 60 letters, digits, hyphens, underscores, and dots.</td></tr>
<tr>
<td>Admin Username</td>
<td>The default value is `root`.</td></tr>
<tr>
<td>Password</td>
<td>The password can contain 8–64 characters in at least three of the following character types: uppercase letters, lowercase letters, digits, and symbols <code>~!@#$%^&amp;*_-+=|\(){}[]:;'&lt;&gt;,.?/</code>.</td></tr>
<tr>
<td>Default Character Set</td>
<td>UTF8, GBK, LATIN1, and UTF8MB4 are supported.</td></tr>
<tr>
<td>Custom Port</td>
<td>It is 3306 by default and can be customized.</td></tr>
</tbody></table>
 - **Advanced Configuration**
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
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
4. After the purchase is completed, you will be redirected to the cluster list. After the status of the cluster becomes **Running**, it can be used normally.

