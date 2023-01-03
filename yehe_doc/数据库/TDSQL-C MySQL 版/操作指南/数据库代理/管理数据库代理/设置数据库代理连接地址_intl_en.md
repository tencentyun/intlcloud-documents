This document describes how to set the database proxy access address in the TDSQL-C for MySQL console.

The database proxy access address is independent of the original database access address. Requests proxied at the proxy address are all relayed through the proxy cluster to access the source and replica nodes of the database. Read/Write requests are separated, so that read requests are forwarded to read-only instances, which lowers the load of the source database.

## Prerequisite
You have enabled the database proxy. For more information, see [Enabling Database Proxy](https://www.tencentcloud.com/document/product/1098/49999).

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql). In the cluster list, click the ID or **Manage** in the **Operation** column of the cluster with the proxy enabled to enter the cluster management page.
2. On the cluster management page, select the **Database Proxy** tab and click the <img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;"> icon next to **Database Proxy Address** on the **Connection Address** tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/NpUQ730_17.png)
<table>
<thead><tr><th width=15%>Item</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Database Proxy Address</td>
<td>It is independent of the original database access address. Proxied requests are all relayed through the proxy cluster to access the source and replica nodes of the database. It can be edited.</td></tr>
<tr>
<td>Network</td>
<td>You can switch the instance's network type between classic network and VPC according to your business needs. <ul><li>In the classic network, instances cannot be isolated through the network but rely on their own allowlist policies to block unauthorized access. </li><li>A VPC is an isolated network environment and has a higher security level.</li></ul></td></tr>
<tr>
<td>Remarks</td>
<td>It is a short description of the database proxy address for easier management.</td></tr>
</tbody></table>
3. In the pop-up dialog box, modify the proxy address and click **OK**.
>!Modifying the proxy address affects the database business being accessed. We recommend you modify the address during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VDRR796_18.png)
