A database instance is a standalone database environment running in Tencent Cloud. It can contain multiple user-created databases and can be accessed using the same tools and applications as those for a standalone database instance.

There are three types of instances available in TencentDB for MySQL:

<table>
<thead>
<tr>
<th>Instance Type</th>
<th width="20%">Definition</th>
<th width="15%">Architecture</th>
<th>Visible in Instance List</th>
<th>Feature</th>
</tr>
</thead>
<tbody><tr>
<td>Master instance</td>
<td>An instance that can be read from and written to</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Basic Edition</a> <li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">High-Availability Edition</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Finance Edition</a></td>
<td>Yes</td>
<td>A master instance can mount read-only instances and disaster recovery instances for read/write separation and remote disaster recovery</td>
</tr>
<tr>
<td>Read-only instance</td>
<td>An instance that can only be read from</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Single-node High IO Edition</a></td>
<td>Yes</td>
<td>A read-only instance cannot exist on its own; instead, it must be affiliated to a master instance. Its data comes solely from sync with the master instance. Besides, it must reside in the same region as the master instance</td>
</tr>
<tr>
<td>Disaster recovery instance</td>
<td>An instance that supports disaster recovery across AZs and regions</td>
<td><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">High-Availability Edition</a><li> <a href="https://intl.cloud.tencent.com/document/product/236/17136" target="_blank">Finance Edition</a></td>
<td>Yes</td>
<td>A disaster recovery instance is read-only during sync with a master instance. It can actively stop the sync and be promoted to a master instance for read/write access. It must reside in a different region from the master instance</td>
</tr>
</tbody></table>

### Related Information
- For more information on how to create read-only instances and related notes, please see [Creating Read-only Instance](https://intl.cloud.tencent.com/document/product/236/7270).
- For more information on how to create and configure RO groups for read-only instances, please see [Managing Read-only Instance](https://intl.cloud.tencent.com/document/product/236/11361).
- For more information on how to create disaster recovery instances and related notes, please see [Creating Disaster Recovery Instance](https://intl.cloud.tencent.com/document/product/236/7272).
