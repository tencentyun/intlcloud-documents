A TencentDB instance is a standalone database environment running in Tencent Cloud. It includes multiple databases created by users and can be accessed using the same tools and applications as those for a standalone database instance.

## Instance Types
TencentDB for PostgreSQL supports the following types of instances:
<table>
<thead><tr><th>Instance Type</th><th width="20%">Definition</th><th width="15%">Architecture</th><th>Visible in the Instance List</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Primary instance</td>
<td>An instance that can be read from and written to</td>
<td>High-Availability edition</td>
<td>Yes</td>
<td>A primary instance can mount read-only instances for read/write separation</td></tr>
<tr>
<td>Read-Only instance</td>
<td>An instance that can only be read from</td>
<td>Single-Node read-only</td>
<td>Yes</td>
<td>A read-only instance cannot exist on its own. Instead, it must be affiliated to a primary instance. Its data comes solely from syncing with the primary instance, and it must reside in the same region as the primary instance. By default, you can create up to seven read-only instances for a primary instance. To create more than seven read-only instances, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td></tr>
</tbody></table>

### Reference
- For more information on the creation of and notes on the read-only instance, please see [Creating Read-Only Instances](https://intl.cloud.tencent.com/document/product/409/39545).
- For more information on creating and configuring a read-only instance group (RO group), please see [Managing RO Groups](https://intl.cloud.tencent.com/document/product/409/39546).

## Supported Instance Specifications
<table>
<tr>
<th>Edition</th><th>Version</th><th>Specification Type</th><th>CPU and MEM</th><th>Disk Capacity</th></tr>
<tr>
<td rowspan="13" width="20%">Dual-Server high-availability edition (one primary and one standby)<br>Read-Only instance</td>
<td rowspan="13" width="12%">10, 11, and 12</td>
<td rowspan="13" width="22%">General - local high-performance SSD</td>
<td>1 core, 2 GiB</td>
<td>10-2,000 GB</td></tr>
<tr>
<td>2 cores, 4 GiB</td><td>10-2,000 GB</td></tr>
<tr>
<td>2 cores, 6 GiB</td><td>10-2,000 GB</td></tr>
<tr>
<td>4 cores, 8 GiB</td><td>10-2,000 GB</td></tr>
<tr>
<td>4 cores, 16 GiB</td><td>10-2,500 GB</td></tr>
<tr>
<td>6 cores, 24 GiB</td><td>10-3,000 GB</td></tr>
<tr>
<td>8 cores, 32 GiB</td><td>10-3,500 GB</td></tr>
<tr>
<td>8 cores, 48 GiB</td><td>10-4,000 GB</td></tr>
<tr>
<td>12 cores, 64 GiB</td><td>1,000-4,500 GB</td></tr>
<tr>
<td>16 cores, 96 GiB</td><td>1,000-5,000 GB</td></tr>
<tr>
<td>20 cores, 128 GiB</td><td>1,000-5,500 GB</td></tr>
<tr>
<td>28 cores, 240 GiB</td><td>1,000-6,000 GB</td></tr>
<tr>
<td>48 cores, 480 GiB</td><td>1,000-6,000 GB</td></tr>
</table>

