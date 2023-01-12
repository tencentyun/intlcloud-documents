After database proxy is enabled for TencentDB for MySQL, a database proxy connection address will be added by default. You can also add connection addresses later to implement different business logics. The number of connection addresses that can be created is the same as that of database proxy nodes. You can view and modify the access policy of a connection address in the console.

## Prerequisites
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/236/42052).

## Viewing the access policy
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Access Policy**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/T4hu809_12.png)

## Modifying the access policy
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), select the region at the top of the page, and click the ID of the target instance to enter the instance management page.
2. On the instance management page, select **Database Proxy** > **Access Policy**, find the target access policy, and click **Settings**.
>? You can also find the target access address in **Database Proxy** > **Overview** > **Connection Address**. Then, click **Adjust Configurations** in the **Operation** column.
>
3. In the pop-up window, modify the policy configuration and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Axkx768_13.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Read-Write Attribute</td>
<td>Modify the read-write attribute of the proxy access address, which can be **Read/Write Separation** or **Read-Only**.</td></tr>
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
