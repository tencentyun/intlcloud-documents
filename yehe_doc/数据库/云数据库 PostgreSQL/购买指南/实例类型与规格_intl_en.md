A TencentDB instance is a standalone database environment running in Tencent Cloud. It includes multiple databases created by users and can be accessed using the same tools and applications as those for a standalone database instance.

## Instance Types
TencentDB for PostgreSQL supports the following types of instances:
<table>
<thead><tr><th>Instance Type</th><th width="20%">Definition</th><th width="15%">Architecture</th><th>Visible in the Instance List</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Primary instance</td>
<td>An instance that can be read from and written to</td>
<td>High-availability edition</td>
<td>Yes</td>
<td>A primary instance can mount read-only instances for read/write separation</td></tr>
<tr>
<td>Read-only instance</td>
<td>An instance that can only be read from</td>
<td>Single-node read-only</td>
<td>Yes</td>
<td>A read-only instance cannot exist on its own. It must instead be associated with a primary instance, with its data only being synced from the primary instance. It must also reside in the same region as the primary instance. By default, up to seven read-only instances can be created for a primary instance. To create more than six read-only instances, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td></tr>
</tbody></table>

### Reference
- For more information on the creation of read-only instances, see [Overview](https://intl.cloud.tencent.com/document/product/409/39545).
- For more information on how to create and configure a read-only instance group (RO group), see [Managing RO Groups](https://intl.cloud.tencent.com/document/product/409/3954).

>!When the used capacity of the instance exceeds the purchased capacity, the database instance will be set to “Read-Only”. You can set alarms for capacity usage.

## Supported Instance Specifications
<table>
<tr>
<th>Edition</th><th>Version</th><th>Specification Type</th><th>CPU and MEM</th><th>Disk Capacity</th><th>Maximum Number of Connections</th><th>
<tr>
<td rowspan="13" width="20%">Dual-server high-availability edition (one-primary-one-standby)<br>Read-only instance</td>
<td rowspan="13" width="12%">10、11、12、13、14</td>
<td rowspan="13" width="22%">General - local high-performance SSD</td>
<td>1-core 2 GiB</td><td>10 GB - 2000 GB</td><td>200</td></tr>
<tr>
<td>2-core 4 GiB</td><td>10 GB - 2000 GB</td><td>400</td></tr>
<tr>
<td>2-core 6 GiB</td><td>10 GB - 2000 GB</td><td>500</td></tr>
<tr>
<td>4-core 8 GiB</td><td>10 GB - 2000 GB</td><td>800</td></tr>
<tr>
<td>4-core 16 GiB</td><td>10 GB - 2500 GB</td><td>1500</td></tr>
<tr>
<td>6-core 24 GiB</td><td>10 GB - 3000 GB</td><td>1800</td></tr>
<tr>
<td>8-core 32 GiB</td><td>10 GB - 3500 GB</td><td>2000</td></tr>
<tr>
<td>8-core 48 GiB</td><td>10 GB - 4000 GB</td><td>2500</td></tr>
<tr>
<td>12-core 64 GiB</td><td>1000 GB - 4500 GB</td><td>3000</td></tr>
<tr>
<td>16-core 96 GiB</td><td>1000 GB - 5000 GB</td><td>5000</td></tr>
<tr>
<td>20-core 128 GiB</td><td>1000 GB - 5500 GB</td><td>10000</td></tr>
<tr>
<td>28-core 240 GiB</td><td>1000 GB - 6000 GB</td><td>13000</td></tr>
<tr>
<td>48-core 480 GiB</td><td>1000 GB - 6000 GB</td><td>22000</td></tr>
</table>
