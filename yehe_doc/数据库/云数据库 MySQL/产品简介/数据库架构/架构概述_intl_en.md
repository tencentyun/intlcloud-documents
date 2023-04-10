TencentDB for MySQL supports three types of architectures: single-node (cloud disk edition), two-node (formerly high availability edition), and three-node (formerly finance edition).
>?The single-node architecture of cloud disk edition is currently supported in Shanghai, Chengdu, Guangzhou, Beijing, and Hong Kong (China) regions and will be available in more regions in the future.
>
## Viewing the instance architecture
- For instances to be purchased, enter the [TencentDB for MySQL purchase page](https://buy.cloud.tencent.com/cdb), and select the architecture in the **Architecture** section.
- For purchased instances, log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), find the target instance from the instance list, and view its architecture in the **Configuration Info** section.

## Architecture comparison
<table>
<thead>
<tr><th>Architecture</th><th >Two-node</th><th>Three-node</th><th colspan=2>Single-node</th>
</thead>
<tbody><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794">Resource isolation policy</a></td>
<td>General</td><td>General</td><td>General (read-only instance)</td><td>Basic</td></tr>
<tr>
<td>Supported version</td>
<td>MySQL 5.5, 5.6, 5.7, 8.0</td><td>MySQL 5.6, 5.7, 8.0</td><td>MySQL 5.6, 5.7, 8.0</td><td>MySQL 5.7, 8.0</td></tr>
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
<td>Local NVMe SSD</td><td>Local NVMe SSD</td><td>Local NVMe SSD</td><td>SSD cloud disk<br>Enhanced SSD cloud disk</td></tr>
<tr>
<td>Performance</td>
<td>Up to 240,000 IOPS</td><td>Up to 240,000 IOPS</td><td>Up to 240,000 IOPS</td><td><li>Random IOPS formula for SSD cloud disk: <br>min{1800 + 30 * capacity (GB), 26000}<li>Throughput formula for SSD cloud disk (MB/s):<br>min{120 + 0.2 * capacity (GB), 260}<li>Random IOPS formula for Enhanced SSD cloud disk: <br>min{1800 + 50 * capacity (GB), 50000}<li>Throughput formula for Enhanced SSD cloud disk (MB/s): <br>min{120 + 0.5 * capacity (GB), 350}</td></tr>
<tr>
<td>Scenario</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Applications with read/write separation requirements</td>
<td>Personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing</td></tr>
</tbody></table>

## References
- TencentDB for MySQL supports MySQL 5.5, 5.6, 5.7, and 8.0. For more information, see [Database Versions](https://intl.cloud.tencent.com/document/product/236/31896).
- TencentDB for MySQL supports the following instance types: the source instance, the read-only instance, and the disaster recovery instance. For more information, see [Database Instance Types](https://intl.cloud.tencent.com/document/product/236/7268).
- TencentDB for MySQL supports different features in different architectures. For more information, see [List of Feature Differences](https://intl.cloud.tencent.com/document/product/236/36007).
