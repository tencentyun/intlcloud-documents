## Product features
This document compares the current and upcoming features supported by different types of TencentDB for MySQL instances, allowing you to learn more about the capabilities of each type, try out latest features, and purchase instances that best suit your needs.
>?
>- "-" in the table means "unsupported".
>- You can click the table title to switch between the feature comparison and new feature list.

<table >
<thead><tr><th>Feature Category</th><th>Feature</th><th>Two-Node</th><th>Three-Node</th><th colspan = "2" >Single-Node</th></tr></thead>
<tbody>
<tr>
<td rowspan="10">Lifecycle</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/39794" target="_blank">Isolation policy</a></td><td>General and dedicated</td><td>General and dedicated</td><td>General (read-only instance)</td><td>Basic (cloud disk edition)</td></tr>
<tr>
<td>Supported versions</td><td><li>MySQL 5.5</li><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td><li>MySQL 5.6</li><li>MySQL 5.7</li><li>MySQL 8.0</li></td><td>MySQL 5.7 and 8.0</td></tr>
<tr>
<td>Node quantity</td><td>2</td><td>3</td><td>1</td><td>1</td></tr>
<tr>
<td>Memory/Disk</td><td>Up to 720 GB/12 TB</td><td>Up to 720 GB/12 TB</td><td>Up to 720 GB/12 TB</td><td>Up to 16 GB/30 TB</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37785" target="_blank">Instance creation</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7270" target="_blank">Read-only instance creation</a></td><td>Supported (for MySQL 5.6, 5.7, and 8.0 only)</td><td>Supported</td><td>Supported</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7272" target="_blank">Disaster recovery instance creation</a></td><td>Supported (for MySQL 5.6, 5.7, and 8.0 only)</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31895" target="_blank">Instance termination</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/52515" target="_blank">Switch from pay-as-you-go to monthly subscription</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47702" target="_blank">Automatic renewal</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan="4">Instance management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/10929" target="_blank">Instance maintenance time configuration</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8460" target="_blank">Instance project configuration</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/19707" target="_blank">Configuration adjustment</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/44337" target="_blank">AZ migration</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">Version upgrade</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8126" target="_blank">Database engine version upgrade</a></td><td>Supported (for MySQL 5.5 and 5.6 only)</td><td>Supported</td><td>Supported</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/36816" target="_blank">Kernel minor version upgrade</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td>Architecture upgrade</td><td><a href="https://intl.cloud.tencent.com/document/product/236/35986" target="_blank">Two-node upgrade to three-node</a></td><td>Supported</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">Supported engines</td>
<td>InnoDB</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47015" target="_blank">RocksDB</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="7">Backup and rollback</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">Automatic backup</a></td><td>Supported</td><td>Supported</td><td>-</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">Manual backup</a></td><td>Supported</td><td>Supported</td><td>-</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38326" target="_blank">Backup deletion</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38864" target="_blank">Instance cloning</a></td><td>Supported</td><td>Supported</td><td>-</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/7276" target="_blank">Rollback</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/37796" target="_blank">Archive backup retention</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://www.tencentcloud.com/document/product/236/51881" target="_blank">Backup encryption</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="4">Monitoring and alarms</td>
<td>Resource monitoring</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td>Engine monitoring</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td>Deployment monitoring</td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td>Alarm</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan="6">Account management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31900" target="_blank">Account creation</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/49197" target="_blank">Password complexity configuration</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31901" target="_blank">Password resetting</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31902" target="_blank">Account permission modification</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31903" target="_blank">Access host address modification</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/31904" target="_blank">Account deletion</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td>Database management</td><td><a href="https://intl.cloud.tencent.com/document/product/236/39221">DMC</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan="4">Data security</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/14470">Security group</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/43496">Database audit</a></td><td>Supported (for MySQL 5.6 and 5.7 only)</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/38491">TDE configuration</a></td><td>Supported (for MySQL 5.7 and 8.0 only)</td><td>Supported (for MySQL 5.7 and 8.0 only)</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/48452">SSL encryption configuration</a></td><td>Supported (for MySQL 5.6, 5.7, and 8.0 only)</td><td>Supported (for MySQL 5.6, 5.7, and 8.0 only)</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="3">Data channel</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8463">Migration with DTS</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8464">Offline migration</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/8466">SQL file import</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td rowspan="2">Parameter management</td>
<td><a href="https://intl.cloud.tencent.com/document/product/236/35793">Instance parameter configuration</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/236/47701">Intelligent parameter tuning</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
<tr>
<td>Network</td><td><a href="https://intl.cloud.tencent.com/document/product/236/31915">Network switch</a></td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan="1">Performance</td><td><a href="https://www.tencentcloud.com/document/product/236/42048">Database proxy (new version)</a></td><td>Supported</td><td>Supported</td><td>-</td><td>-</td></tr>
</tbody>
</table>
