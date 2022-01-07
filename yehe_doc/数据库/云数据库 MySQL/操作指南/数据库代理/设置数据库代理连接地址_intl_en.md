
This document describes how to set the database proxy access address in the TencentDB for MySQL console.

The database proxy access address is independent of the original database access address. Requests proxied at the proxy address are all relayed through the proxy cluster to access the source and replica nodes of the database. Read/Write separation is implemented, so that read requests are forwarded to read-only instances, which lowers the load of the source database.

## Prerequisites
You have [enabled database proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, select the source instance for which to enable database proxy and click its ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Database Proxy** tab and click the <img src="https://main.qcloudimg.com/raw/be716b5360d5256a9d5e816e29872ec1.png"  style="margin:0;"> icon next to **Connection Address**.
![](https://main.qcloudimg.com/raw/63015c402bdd31e04e2597af84013a74.png)
<table>
<thead><tr><th width=15%>Term</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Database proxy address</td>
<td>It is independent of the original database access address. Proxied requests are all relayed through the proxy cluster to access the source and replica nodes of the database. It can be edited.</td></tr>
<tr>
<td>Network type</td>
<td>You can switch the instance's network type between classic network and VPC according to your business needs. <ul><li>In the classic network, instances cannot be isolated through the network but rely on their own allowlist policies to block unauthorized access. </li><li>A VPC is an isolated network environment and has a higher security level.</li></ul></td></tr>
<tr>
<td>Remarks</td>
<td>It is a short description of the database proxy address for easier management.</td></tr>
</tbody></table>
3. In the pop-up window, modify the proxy address and click **OK**.
>!Modifying the private network address affects the database business being accessed. We recommend you modify the address during off-peak hours. Make sure that your business has a reconnection mechanism.
>
![](https://main.qcloudimg.com/raw/982fd53d880ab1a6d4f8df0372a99613.png)
