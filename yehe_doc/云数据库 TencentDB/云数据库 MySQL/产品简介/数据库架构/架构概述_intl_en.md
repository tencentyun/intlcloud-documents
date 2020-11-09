TencentDB for MySQL supports four types of architectures: the High-availability Edition, the Finance Edition, the Single-node High IO Edition, and the Basic Edition. Currently, the Single-node High IO Edition applies to [read-only instances](https://intl.cloud.tencent.com/document/product/236/7270) only.

## Viewing Instance Architectures
- For instances to be purchased, log in to the [TencentDB for MySQL purchase page](https://buy.cloud.tencent.com/cdb) and select the architecture in the "Architecture" section.
![](https://main.qcloudimg.com/raw/f1417a645690900e4d82515e8e609d3b.png)
- For purchased instances, log in to the [MySQL console](https://console.cloud.tencent.com/cdb), locate the desired instance in the instance list, and view its architecture in the "Configuration" column.
![](https://main.qcloudimg.com/raw/0f5f39c3eeb7bdbcd61d6ccf157c07b2.png)


## Architecture Comparison

<table>
<thead>
<tr>
<th width="15%">Architecture</th>
<th width="20%">High-availability Edition</th>
<th width="20%">Finance Edition</th>
<th width="20%">Single-node High IO Edition</th>
<th width="25%">Basic Edition</th>
</tr>
</thead>
<tbody><tr>
<td>Supported Version</td>
<td>MySQL v5.5, v5.6, v5.7, and v8.0</td>
<td>MySQL v5.6, v5.7, and v8.0</td>
<td>MySQL v5.6, v5.7, and v8.0</td>
<td>MySQL v5.7</td>
</tr>
<tr>
<td>Node</td>
<td>One source node, one replica node</td>
<td>One source node, two replica nodes</td>
<td>Single node</td>
<td>Single node</td>
</tr>
<tr>
<td>Source-replica Replication Mode</td>
<td>Async (default), semi-sync</td>
<td>Strong sync</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>Instance Availability</td>
<td>99.95%</td>
<td>99.99%</td>
<td>-</td>
<td>-</td>
</tr>
<tr>
<td>Underlying Storage</td>
<td>Local NVMe SSD</td>
<td>Local NVMe SSD</td>
<td>Local NVMe SSD</td>
<td>Premium cloud disk</td>
</tr>
<tr>
<td>Performance</td>
<td>Up to 240,000 IOPS</td>
<td>Up to 240,000 IOPS</td>
<td>-</td>
<td>The IOPS calculation formula: <br>{min 1,500 + 8 * capacity, max 4,500}</td>
</tr>
<tr>
<td>Use Case</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Gaming, internet, IoT, retail, e-commerce, logistics, insurance, securities, etc.</td>
<td>Applications with read/write separation requirements</td>
<td>Personal learning, small websites, non-core small enterprise systems, and medium-to-large enterprise development and testing</td>
</tr>
</tbody></table>

## Documentation
- TencentDB for MySQL supports MySQL v8.0, v5.7, v5.6, and v5.5. For more information, please see [Database Version](https://intl.cloud.tencent.com/document/product/236/31896).
- TencentDB for MySQL supports the following instance types: the source instance, the read-only instance, and the disaster recovery instance. For more information, please see [Database Instance Types](https://intl.cloud.tencent.com/document/product/236/7268).
- TencentDB for MySQL supports different features in different architectures. For more information, please see [List of Feature Differences](https://intl.cloud.tencent.com/document/product/236/36007).
