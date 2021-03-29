TencentDB for MySQL supports three types of architectures: single-node (formerly Basic Edition), two-node (formerly High IO Edition), and three-node (formerly Finance Edition).
>?General single-node instances are formerly known as Single-node High IO Edition instances.

## Viewing Instance Architectures
- For instances to be purchased, log in to the [TencentDB for MySQL purchase page](https://buy.cloud.tencent.com/cdb) and select the architecture in the **Architecture** section.
- For purchased instances, log in to the [MySQL console](https://console.cloud.tencent.com/cdb), locate the desired instance in the instance list, and view its architecture in the **Configuration** column.

## Architecture Comparison
<table>
<thead>
<tr><th>Architecture</th><th >Two-node</th><th>Three-node</th><th colspan=2>Single-node</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">Resource isolation policy</a></td>
<td>General</td><td>General</td><td>General</td><td>Basic</td></tr>
<tr>
<td>Supported version</td>
<td>MySQL 5.5, 5.6, 5.7, and 8.0</td><td>MySQL 5.6, 5.7, and 8.0</td><td>MySQL 5.6, 5.7, and 8.0</td><td>MySQL 5.7</td></tr>
<tr>
<td>Node</td>
<td>One source, one replica</td><td>One source, two replicas</td><td>Single node</td><td>Single node</td></tr>
<tr>
<td>Source-replica replication mode</td>
<td>Async (default), semi-sync</td><td>Async (default), strong sync, and semi-sync</td><td>-</td><td>-</td></tr>
<tr>
<td>Instance availability</td>
<td>99.95%</td><td>99.99%</td><td>-</td><td>-</td></tr>
<tr>
<td>Underlying storage</td>
<td>Local NVMe SSD</td><td>Local NVMe SSD</td><td>Local NVMe SSD</td><td>Premium cloud disk</td></tr>
<tr>
<td>Performance</td>
<td>Up to 240,000 IOPS</td><td>Up to 240,000 IOPS</td><td>-</td><td>IOPS calculation formula: <br>{min 1,500 + 8 x disk capacity, max 4,500}</td></tr>
<tr>
<td>Use cases</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Applications with read/write separation requirements</td>
<td>Personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing</td></tr>
</tbody></table>

## Documentation
- TencentDB for MySQL supports MySQL 8.0, 5.7, 5.6, and 5.5. For more information, please see [Database Versions](https://intl.cloud.tencent.com/document/product/236/31896).
- TencentDB for MySQL supports the following instance types: source instances and read-only replicas. For more information, please see [Database Instance Types](https://intl.cloud.tencent.com/document/product/236/7268).
- TencentDB for MySQL supports different features in different architectures. For more information, please see [List of Feature Differences](https://intl.cloud.tencent.com/document/product/236/36007).
