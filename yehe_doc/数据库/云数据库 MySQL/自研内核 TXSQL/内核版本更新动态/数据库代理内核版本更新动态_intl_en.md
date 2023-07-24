This document describes the kernel version updates of the TencentDB for MySQL database proxy.
>?If the MySQL kernel version requirements are not met, you can upgrade the kernel version of your database first as instructed in [Upgrading Kernel Minor Version](https://www.tencentcloud.com/document/product/236/36816?lang=en&pg=).
>
<table>
<thead>
<tr>
<th >Database Proxy Version</th>
<th>MySQL Kernel Version Requirements</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>1.3.7</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Fixes</strong><li>Fixed the routing error of the `select for update` statement in some cases</li><li>Modified the `select @@read_only` statement and made it possible to be routed to the source database. This prevents some frameworks that use read_only flags from misjudging the database proxy as unwritable.</li><li>Fixed the database proxy node exceptions caused by a database instance HA in some scenarios.</li></td>
</tr>
<tr>
<td>1.3.4</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Fixes</strong><br>Fixed the issue where the 'show processlist' command returned incomplete data</td>
</tr>
<tr>
<td>1.3.3</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Fixes</strong><br>Fixed the issue where an error was reported when the session connection pool reused connections to send `change_user` to the backend, and the issue where the `PREPARE` statement was not correctly handled by the database proxy after a new connection was established.</td>
</tr>
<tr>
<td>1.3.2</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Fixes</strong><br>Fixed the issue where `execute` statement didn't have a parameter type</td>
</tr>
<tr>
<td>1.3.1</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Feature updates</strong><li>Allowed instances with a weight of 0 to sustain read requests when the weight of all valid instances under the database proxy is 0. </li><li>Supported the multi-AZ deployment architecture where read-only instances can be mounted across AZs. </li><li>Provided the read-only mode. </li><li>Supported transaction split. </li><li>Supported momentary disconnection prevention, i.e., connection persistence, where the client will not be disconnected when a database instance HA switch occurs because of a scheduled task. </li></td>
</tr>
<tr>
<td>1.2.1</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Feature updates</strong><li>Supported the `db lower_case_table_names` parameter, indicating not to verify the letter case by default. </li><li>Supported returning error messages in the query stage when errors occur during database proxy connection establishment. </li></td>
</tr>
<tr>
<td>1.1.3</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211202 or later</li></td>
<td><strong>Feature updates</strong><br>Supported the use of hint routing information in the `COM_PREPARE` packet preprocessed by MySQL. After hint is used in `PREPARE` to specify the routing target, subsequent `execute` packets will be sent to the specified backend node. <br><strong>Fixes</strong><li>Fixed the issue where the frontend connection was reset immediately after source-replica switch of the source instance on the database proxy was performed. </li><li>Fixed the issue where load balancing might fail when read-only instances exceeded the latency threshold. Routing will resume normally when the read-only instance latency falls below the threshold. </li><li>Fixed the issue where MySQL 8.0 might return incorrect handshake information and cause connection failures.</li></td>
</tr>
<tr>
<td>1.1.2</td>
<td><li>MySQL 5.7 20211030 or later</li><li>MySQL 8.0 20211130 or later</li></td>
<td><strong>Feature updates</strong><li>Supported MySQL 8.0. </li><li>Supported the connection pool feature at the connection level, which is useful in scenarios where non-persistent connections to the database are frequently established. The database proxy will save connections and reuse them during subsequent connection establishments. </li><li>Supported the reconnection feature for read-only instances. In persistent connection scenarios, when a read-only instance is restarted or added, the database proxy will automatically establish a connection and restore routing to it. </li><li>Updated the internal memory management mechanism to reduce the memory usage.<br><strong>Fixes</strong></li><li>Fixed the issue where the client connection persisted after the backend connection was closed due to timeout. </li><li>Fixed the issue where the internal cache might cause excessively rapid increase of the memory utilization. </li><li>Fixed the occasional issue where packets in an incorrect format were returned.</li></td>
</tr>
<tr>
<td>1.0.1</td>
<td>MySQL 5.7 20201230 or later</td>
<td><strong>Feature updates</strong><li>Supported MySQL 5.7. </li><li>Supported read/write separation. </li><li>Supported read weight assignment in read/write separation. </li><li>Supported the configuration of source-replica replication delay threshold. Routing to a read-only instance will be stopped if its delay exceeds the thresholds and will be recovered after it drops below the threshold. If the source-replica replication is interrupted, disconnected read-only instances will be removed directly. </li><li>Supported the configuration of the least number of read-only instances. When read-only instances are removed, if the number is set to N, at least N instance(s) will be retained for routing. </li><li>Supported the failover configuration, which is enabled by default. If it is disabled and the read weight of the source instance is 0, after all read-only instances are removed, an error will be reported for read requests. If failover is enabled and the read weight of the source instance is not 0, requests will be routed to the source instance. </li><li>Supported using the HINT syntax to specify routing nodes.</li></td>
</tr>
</tbody></table>