A TencentDB for MySQL instance is a database environment that runs independently in Tencent Cloud. It is the basic unit for you to purchase the TencentDB for MySQL service. You can create, modify, and delete instances in the console.
Each instance is independent of each other with isolated resources. There are no CPU, memory, and IO preemption issues between instances. Each instance has its own characteristics such as database type and version, and the system has corresponding parameters to control instance behaviors.

There are three types of instances available in TencentDB for MySQL:

<table>
<thead><tr>
<th>Instance Type</th><th width="20%">Definition</th><th width="15%">Architecture</th><th>Visible in Instance List</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Source instance</td><td>An instance that can be read from and written to</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Single-node</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Two-node</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">Three-node</a></td>
<td>Yes</td><td>A source instance can mount read-only instances and disaster recovery instances for read/write separation and remote disaster recovery.</td></tr>
<tr>
<td>Read-only instance</td><td>An instance that can only be read from</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Single-node</a></td><td>Yes</td>
<td>A read-only instance cannot exist on its own. Instead, it must be affiliated to a source instance. Its data comes solely from syncing with the source instance, and it must reside in the same region as the source instance.</td></tr>
<tr>
<td>Disaster recovery instance</td><td>An instance that supports disaster recovery across AZs and regions</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Two-node</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">Three-node</a><td>Yes</td>
<td>A disaster recovery instance is read-only when it syncs with a source instance. It can actively stop the sync and be promoted to a source instance for read/write access. The disaster recovery instance should reside in a different region than the source instance does.</td></tr>
</tbody></table>

### Reference
- For more information on the creation of read-only instances, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/7270).
- For more information on how to create and configure RO groups for read-only instances, see [Managing the RO Group of Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/11361).
- For more information on the creation of and notes on the disaster recovery instance, see [Managing Disaster Recovery Instance](https://intl.cloud.tencent.com/document/product/236/7272).
