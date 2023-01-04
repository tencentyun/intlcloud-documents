This document describes the release notes of the TDSQL-C for MySQL database proxy.

## Viewing the database proxy version
You can view the version in **Overview** > **Proxy Version** on the [Database Proxy](https://www.tencentcloud.com/document/product/1098/49999) tab.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QRQp279_6.png)

## Version description
<table>
<tr>
<th>Version</th>
<th>Description</th>
</tr>
<tr>
<td>1.2.1</td>
<td><strong>Feature updates</strong><ul><li>Supported MySQL 5.7/8.0.</li><li>Supported cluster deployment to deploy multiple instances under one database proxy.</li><li>Supported read/write separation and corresponding weight configuration.</li><li>Supported the failover feature to send read requests to the read-write instance in case of read-only instance failures.</li><li>Supported the load balancing feature to balance the connections to each proxy node.</li><li>Supported using the HINT syntax to specify router nodes.</li><li>Supported the session-level connection pool for scenarios where non-persistent connections were frequently established to the database.</li><li>Allowed the database proxy to save connections and reuse them subsequently.</li><li>Supported hot loading to modify configurations online without restarting the dedicated database proxy.</li><li>Supported the reconnection feature for read-only instances. In persistent connection scenarios, when a read-only instance was restarted or added, the database proxy would automatically establish a connection and restore routing to it.</li></ul></td>
</tr>
</table>
