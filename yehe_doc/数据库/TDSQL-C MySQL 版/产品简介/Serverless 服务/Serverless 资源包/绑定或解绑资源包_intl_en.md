If you want to use a resource pack, you need to bind the resource pack after purchasing it. You can also unbind a resource pack that has been bound to clusters. This document describes how to bind or unbind a resource pack.
>? A resource pack can be bound to multiple serverless clusters, but a serverless cluster can only be bound to up to one compute resource pack and one storage resource pack.
## Prerequisites
- You have created a serverless cluster. For more information, see [Creating Serverless Cluster](https://www.tencentcloud.com/document/product/1098/51976).
- You have purchased a resource pack. For more information, see [Purchasing Resource Pack](https://www.tencentcloud.com/document/product/1098/55247).

## Binding a resource pack[](id:BDZYB)
### Scenario 1: Binding a resource pack when creating a serverless cluster
1. Go to the [purchase page](https://buy.tencentcloud.com/cynosdb?product=package) and complete the **Database Configuration** settings.
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Database Engine</td>
<td>Select **MySQL**. </td></tr>
<tr>
<td>Database Mode</td>
<td>Select **Serverless**</td> </td></tr>
<tr>
<td>Region</td>
<td>Select a region for database deployment. <dx-alert infotype="explain" title="">
Currently, the serverless mode is supported only in Guangzhou, Shanghai, Beijing, Nanjing, Hong Kong (China), Silicon Valley, and Singapore regions. If you need to use it in other regions, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
</dx-alert></td></tr>
<tr>
<td>Source AZ</td>
<td>Select an AZ for deployment. The available AZs are as displayed on the purchase page. </td></tr>
<tr>
<td>Multi-AZ Deployment</td>
<td>Currently, serverless instances don't support multi-AZ deployment. </td></tr>
<tr>
<td>Network</td>
<td>For performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C for MySQL instances only in the same <a href="https://www.tencentcloud.com/document/product/215">VPC</a>. </td></tr>
<tr>
<td>Compatible Database</td>
<td>MySQL 5.7 and 8.0 are now supported. </td></tr>
<tr>
<td>Compute Unit</td>
<td>Select the upper and lower limits of the TDSQL-C Compute Unit (CCU), and the instance will be automatically and elastically scaled within the selected resource range. <dx-alert infotype="explain" title="">
CCU is the computing and billing unit for the serverless mode. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater of the number of CPU cores used by the database and 1/2 of the memory size. For more information, see <a href="https://www.tencentcloud.com/document/product/1098/51975">Compute Unit</a>. </td></tr>.
</dx-alert></td></tr>
<tr>
<td>Auto-Pause</td>
<td>Configure the automatic pause time of the instance. If there is no connection to access the database within the set time, the instance will be automatically paused, with billing stopped. </td></tr>
</tbody></table>


2. After completing the **Specification Billing** configuration, click **Next**.
>?**Total serverless fees = compute node fees + storage space fees = serverless computing power price x number of CCUs + storage space price x storage space**
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>Compute Billing Mode</td>
<td>Select a resource pack type. <dx-alert infotype="explain" title="">
The compute resource pack will be used preferably for the deduction of actual CCU usage per second. When the pack is used up, the resource usage will be pay-as-you-go. The resource pack mode is more cost-effective and flexible than the pay-as-you-go option.
</dx-alert></td></tr>
<tr>
<td>Compute Resource Pack</td>
<td>You can bind all valid compute resource packs in the region selected by the cluster. If there is no available resource pack, purchase one as instructed in <a href="https://www.tencentcloud.com/document/product/1098/55247">Purchasing Resource Pack</a>. </td></tr>
<tr>
<td>Storage Billing Mode</td>
<td>Select a resource pack type. <dx-alert infotype="explain" title="">
The storage resource pack will be used preferably for the deduction of actual usage per hour. When the pack is used up, the resource usage will be pay-as-you-go. The resource pack mode is more cost-effective and flexible than the pay-as-you-go option.
</dx-alert></td></tr>
<tr>
<td>Storage Resource Pack</td>
<td>You can bind all valid storage resource packs in the region selected by the cluster. If there is no available resource pack, purchase one as instructed in <a href="https://www.tencentcloud.com/document/product/1098/55247">Purchasing Resource Pack</a>. </td></tr>
</tbody></table>


3. Select the number of clusters. You can purchase multiple clusters of the same specification in batches. Then, click **Next**.
4. Complete the **Basic Info** and **Advanced Configuration** settings, confirm the fees, and click **Buy Now**.
 - **Basic Info**
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Cluster Name</td>
<Td> Select one of the options: **Name It Later** or **Name It Now**. The name can contain up to 60 letters, digits, or symbols (<code>-_.</code>). </td></tr>
<tr>
<td>Admin Username</td>
<td>The default value is `root`. </td></tr>
<tr>
<td>Password</td>
<td>The password can contain 8–64 characters in at least three of the following types: uppercase letters, lowercase letters, digits, and symbols (<code>~!@#$%^&amp;*_-+=|\(){}[]:;'&lt;&gt;,.?/</code>). </td></tr>
<tr>
<td>Default Character Set</td>
<td>UTF8, GBK, LATIN1, and UTF8MB4 are supported. </td></tr>
<tr>
<td>Custom Port</td>
<td>It is 3306 by default and can be customized. </td></tr>
</tbody></table>
 - **Advanced Configuration**
<table>
<thead><tr><th width=13%>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Security Group</td>
<td>Select or create a security group. </td></tr>
<tr>
<td>Parameter Template</td>
<td>Select or create a parameter template. </td></tr>
<tr>
<td>Table Name Case Sensitivity</td>
<td>Select **Case-Insensitive** or **Case-Sensitive**. </td></tr>
<tr>
<td>Project</td>
<td>Specify a project for the cluster to be created. </td></tr>
<tr>
<td>Alarm Policy</td>
<td>Select or create an alarm policy. </td></tr>
<tr>
<td>Tag</td>
<td>Add a tag to facilitate resource categorization and management. </td></tr>
<tr>
<td>Terms and Conditions</td>
<td>Read and indicate your consent to the terms and conditions. </td></tr>
</tbody></table>
5. After the purchase is completed, you will be redirected to the [cluster list](https://console.cloud.tencent.com/cynosdb/mysql/ap-beijing/cluster/cynosdbmysql-4fyuay8e/detail). After the cluster is in **Running** status, it can be used normally.
>?
>- If only the compute resource pack is bound, the compute nodes of the serverless cluster will be deducted by using the bound compute resource pack, while the storage nodes will be billed on a pay-as-you-go basis.
>- If only the storage resource pack is bound, the storage nodes of the serverless cluster will be deducted by using the bound storage resource pack, while the compute nodes will be billed on a pay-as-you-go basis.
- If both the compute and storage resource packs are bound, both the compute and storage nodes of the serverless cluster will be deducted by using the bound compute and storage resource packs.

### Scenario 2: Binding a resource pack to an existing serverless cluster
#### Binding a resource pack to an existing serverless cluster in the resource pack list
After purchasing a resource pack, you can bind it to an existing serverless cluster in the resource pack list.
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. On the left sidebar, click **Resource Pack** to enter the resource pack management page.
3. Find the target resource pack directly on the page or quickly filter it out in the search box on the right, and click **Bind/Unbind** in the **Operation** column.
4. In the pop-up window, select a region, select one or more serverless clusters to which the resource pack is bound, and click **OK**.

#### Binding a resource pack to an existing serverless cluster on the cluster management page
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Target Cluster** in the cluster list on the left to enter the cluster management page.
3. On the cluster management page, select **Resource Pack** and click **Bind Resource Pack**.
4. In the pop-up window, select the target resource pack and click **OK**.
>?
>- If only one compute resource pack or one storage resource pack is selected, and the corresponding storage or compute nodes will be billed on a pay-as-you-go basis.
>- Up to one compute resource pack and one storage resource pack can be selected at the same time.

## Unbinding a resource pack
When a resource pack expires or is used up, the resource pack will be automatically unbound. You can also unbind it manually.
#### Unbinding a resource pack from an existing serverless cluster in the resource pack list
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. On the left sidebar, click **Resource Pack** to enter the resource pack management page.
3. Find the target resource pack directly on the page or quickly filter it out in the search box on the right, and click **Bind/Unbind** in the **Operation** column.
4. In the pop-up window, select a region, select the target bound serverless cluster, and click **OK**.

#### Unbinding a resource pack from an existing serverless cluster on the cluster management page
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. Click **Target Cluster** in the cluster list on the left to enter the cluster management page.
3. On the cluster management page, select **Resource Pack**.
4. Find the target resource pack, and click **Unbind** in the **Operation** column.
5. In the pop-up window, click **OK**.
