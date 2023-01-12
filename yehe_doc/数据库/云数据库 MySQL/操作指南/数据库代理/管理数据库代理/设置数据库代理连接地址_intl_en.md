This document describes how to set the database proxy connection address in the TencentDB for MySQL console.

The database proxy connection address is independent of the original database connection address. Requests proxied at the proxy address are all relayed through the proxy cluster to the source and replica nodes of the database, so that read and write requests are separated, with reads being forwarded to read-only instances. In this way, the load of the source database is lowered.
After database proxy is enabled for TencentDB for MySQL, a database proxy connection address will be added by default, and you can also add, modify, or delete the connection address for database proxy.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy] (https://www.tencentcloud.com/document/product/236/42052).

## Modifying Database Proxy Connection Address
1. Log in to the [TencentDB for MySQL console] (https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column of the instance with the proxy enabled to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab and click the <img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;"> icon next to **Private Network Access Address** on the **Connection Address** tab.
![](https://main.qcloudimg.com/raw/63015c402bdd31e04e2597af84013a74.png)
3. In the pop-up dialog box, modify the proxy address and click **OK**.
>!Modifying the proxy address affects the database business being accessed. We recommend you modify the address during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://main.qcloudimg.com/raw/982fd53d880ab1a6d4f8df0372a99613.png)

## Adding Database Proxy Connection Address
>?
>- The number of connection addresses is the same as that of database proxy nodes.
>- An connection address will be created by default when the database proxy is enabled.
>
1. Log in to the [TencentDB for MySQL console] (https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column of the instance with the proxy enabled to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab, and click **Add Access Address** next to **Connection Address**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iVTk464_19.png)
3. In the **Create Connection** window, set the following configuration items and click **OK**.
**Step 1. Configure a network**
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Network</td>
<td>Database proxy only supports VPC. You can choose to automatically assign or specify an address.</td></tr>
<tr>
<td>Security group</td>
<td>The security group of the source instance is selected by default. You can also select another or more existing security groups or create a new one as needed. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Note</div>        <div class="rno-document-tip-desc"><p>To access through the database proxy, you need to configure security group policies and open the private port (3306). For more information, see <a href="https://intl.cloud.tencent.com/document/product/236/14470">TencentDB Security Group Management</a>.</p></div>    </div></blockquote></td></tr>
<tr>
<td>Remarks</td>
<td>Optional. You can add remarks for the new database proxy connection address.</td></tr>
</tbody></table>
<b>Step 2: Configure a policy</b>
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Read-Write Attribute</td>
<td>Select the read-write attribute of the proxy access address, which can be **Read/Write Separation** or **Read-Only**.</td></tr>
<tr>
<td>Remove Delayed RO Instances</td>
<td>Set the **Remove Delayed RO Instances** policy. After this option is enabled, you can set **Delay Threshold** and **Least RO Instances**. The system will try removing or restoring a failed read-only instance no matter whether this option is enabled. <ul><li>**Delay Threshold**: Enter an integer greater than or equal to 1 (in seconds). </li><li>**Least RO Instances**: It is subject to the number of read-only instances owned by the source instance. If it is set to `0`, when all read-only nodes are removed, all read requests will be routed to the source instance until at least one of the removed read-only instances rejoins the database proxy to continue processing the read requests.</li></ul></td></tr>
<tr>
<td>Connection Pool Status</td>
<td>The connection pool feature mainly mitigates the instance load caused by frequent new connections in non-persistent connection business scenarios. After this option is enabled, you can select the supported connection pool type, which currently can only be the session-level connection pool by default.</td></tr>
<tr>
<td>Transaction Split</td>
<td>You can set whether to enable this feature. After it is enabled, reads and writes in one transaction will be separated to different instances for execution, and read requests will be forwarded to read-only instances to reduce the load of the source instance.</td></tr>
<tr>
<td>Assign Read Weight</td>
<td>You can select **Assigned by system** or **Custom**. If multiple AZs are configured when the database proxy is enabled, you can separately assign the weights of proxy nodes in different AZs.</td></tr>
<tr>
<td>Failover (with **Read-Write Attribute** being **Read/Write Separation**)</td>
<td>You can set whether to enable this feature. After it is enabled, if database proxy fails, the database proxy address will route requests to the source instance.</td></tr>
<tr>
<td>Apply to Newly Added RO Instances</td>
<td>You can set whether to enable this feature. After it is enabled, a newly purchased read-only instance will be automatically added to the database proxy. <ul><li>If **Assign Read Weight** is set to **Assigned by system**, newly purchased read-only instances will be assigned with the default weight based on their specification. </li><li>If **Assign Read Weight** is set to **Custom**, when newly purchased read-only instances are added, their weights will be 0 by default, which can be modified by clicking **Adjust Configurations** in **Connection Address** on the **Database Proxy** tab.</li></ul></td></tr>
</tbody></table>

## Deleting Database Proxy Connection Address
>? If your database proxy has multiple connection addresses, you can delete unnecessary ones while keeping the last one.
>
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column of the instance with the proxy enabled to enter the instance management page.
2. On the instance management page, find the target address in **Database Proxy** > **Connection Address**, and click **Disable**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7FDj373_20.png)
3. In the pop-up window, click **OK**.

