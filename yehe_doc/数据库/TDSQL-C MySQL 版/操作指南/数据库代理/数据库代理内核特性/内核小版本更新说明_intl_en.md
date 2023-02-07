This document describes the release notes of the TDSQL-C for MySQL database proxy.

## Viewing database proxy version
On the cluster list page, proceed according to the actually used view mode:
<dx-tabs>
::: Tab view
**Option 1**
On the cluster management page, click **Database Proxy** and view it in **Overview** > **Basic Info** > **Proxy Version**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/m53B997_2.png)
**Option 2**
On the **Cluster Details** tab on the cluster management page, click **Details** after **Database Proxy** in the architecture to enter the **Database Proxy** page, and view it in **Overview** > **Basic Info** > **Proxy Version**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/LKG7904_3.png)
:::
::: List view
You can view the version in **Overview** > **Proxy Version** on the [Database Proxy](https://www.tencentcloud.com/document/product/1098/49999) tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/JVEb093_4.png)
:::
</dx-tabs>



## Version description
>?If the TDSQL-C for MySQL kernel version requirements are not met, you can upgrade the kernel version of your database first as instructed in [Upgrading Kernel Minor Version](https://intl.cloud.tencent.com/document/product/1098/44617).

<table>
<thead><tr><th>Version</th><th>TDSQL-C for MySQL Kernel Version Requirement</th><th>Description</th></tr></thead>
<tbody>
<tr>
<td>1.3.3</td>
<td>TDSQL-C for MySQL 5.7 ≥ 2.0.20/2.1.6<br>TDSQL-C for MySQL 8.0 ≥ 3.1.6</td>
<td><strong>Fixes</strong><ul><li>Fixed the issue where an error was reported when the session connection pool reused connections to send `change_user` to the backend, and the issue where the PREPARE statement was not correctly handled by the database proxy after a new connection was established.</li><li>Fixed the issue where the EXECUTE statement didn't have a parameter type.</li></ul></td></tr>
<tr>
<td>1.2.1</td>
<td>-</td>
<td><strong>Feature updates</strong><ul><li>Supported MySQL 5.7/8.0.</li><li>Supported cluster deployment to deploy multiple instances under one database proxy.</li><li>Supported read/write separation and corresponding weight configuration.</li><li>Supported the failover feature to send read requests to the read-write instance in case of read-only instance failures.</li><li>Supported the load balancing feature to balance the connections to each proxy node.</li><li>Supported using the HINT syntax to specify router nodes.</li><li>Supported the session-level connection pool for scenarios where non-persistent connections were frequently established to the database.</li><li>Allowed the database proxy to save connections and reuse them subsequently.</li><li>Supported hot loading to modify configurations online without restarting the dedicated database proxy.</li><li>Supported the reconnection feature for read-only instances. In persistent connection scenarios, when a read-only instance was restarted or added, the database proxy would automatically establish a connection and restore routing to it.</li></ul></td></tr>
</tbody></table>
