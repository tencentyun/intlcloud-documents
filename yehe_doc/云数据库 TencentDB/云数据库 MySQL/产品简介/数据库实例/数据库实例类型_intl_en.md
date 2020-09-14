A TencentDB instance is a standalone database environment running in Tencent Cloud. It includes multiple databases created by users and can be accessed using the same tools and applications as those for a standalone database instance.

There are three types of instances available in TencentDB for MySQL:

<table>
<thead>
<tr>
<th>Instance Type</th>
<th width="20%">Definition</th>
<th width="15%">Architecture</th>
<th>Visible in the Instance List</th>
<th>Feature</th>
</tr>
</thead>
<tbody><tr>
<td>Source instance</td>
<td>An instance that can be read from and written to</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Basic Edition</a> <li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">High-availability Edition</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Finance Edition</a></td>
<td>Yes</td>
<td>A source instance can mount read-only instances and disaster recovery instances for read/write separation and remote disaster recovery</td>
</tr>
<tr>
<td>Read-only instance</td>
<td>An instance that can only be read from</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Single-node High IO Edition</a></td>
<td>Yes</td>
<td>A read-only instance cannot exist on its own. Instead, it must be affiliated to a source instance. Its data comes solely from syncing with the source instance, and it must reside in the same region as the source instance.</td>
</tr>
<tr>
<td>Disaster recovery instance</td>
<td>An instance that supports disaster recovery across AZs and regions</td>
<td><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">High-availability Edition</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Finance Edition</a></td>
<td>Yes</td>
<td>A disaster recovery instance is read-only when it syncs with a source instance. It can actively stop the sync and be promoted to a source instance for read/write access. The disaster recovery instance should reside in a different region than the source instance does.</td>
</tr>
</tbody></table>

### Related Information
- For more information on the creation of and notes on the read-only instance, please see [Read-Only Instances](https://intl.cloud.tencent.com/document/product/236/7270).
- For more information on how to create and configure a RO group of read-only instances, please see [Creating a RO Group of Read-Only Instances](https://intl.cloud.tencent.com/document/product/236/11361).
- For more information on the creation of and notes on the disaster recovery instance, please see [Disaster Recovery Instances](https://intl.cloud.tencent.com/document/product/236/7272).
