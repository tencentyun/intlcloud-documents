A TencentDB instance is a standalone database environment running in Tencent Cloud. It includes multiple databases created by users and can be accessed by using the same tools and applications as those for a standalone database instance.

There are two types of instances available in TencentDB for MySQL:

<table>
<thead><tr>
<th>Instance Type</th><th width="20%">Definition</th><th width="15%">Architecture</th><th>Visibility in Instance List</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Source instance</td><td>An instance that can be read from and written to</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Single-Node</a> <li><a href="https://intl.cloud.tencent.com/document/product/236/38329" target="_blank">Two-Node</a><li><a href="https://intl.cloud.tencent.com/document/product/236/39783" target="_blank">Three-Node</a></td>
<td>Yes</td><td>A source instance can mount read-only instances for read/write separation</td></tr>
<tr>
<td>Read-Only instance</td><td>An instance that can only be read from</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38331" target="_blank">Single-Node</a></td><td>Yes</td>
<td>A read-only instance cannot exist independently. Instead, it must be affiliated to a source instance. Its data comes solely from syncing with the source instance, and it must reside in the same region as the source instance</td></tr>


### Related Information
- For more information on the creation of read-only instances, see [Creating Read-Only Instance](https://intl.cloud.tencent.com/document/product/236/7270).
- For more information on the management of RO groups, see [RO Group of Read-Only Instances](https://intl.cloud.tencent.com/document/product/236/11361).

  
