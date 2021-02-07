
<table>
<thead>
<tr>
<th width="22%">Instance Architecture</th>
<th>Definition</th>
<th>Node</th>
<th>Features</th>
</tr>
</thead>
<tbody><tr>
<td>Standard Edition (one primary and one replica)</td>
<td>Each shard provides a high-availability architecture based on primary/replica active-active deployment.</td>
<td>Two nodes: one primary node and one replica node</td>
<td rowspan = "2"><li>Supports real-only replicas.</li><li>Automatic node failover.</li><li>Default sampling granularity for monitoring: once every 5 minutes.</li><li>Maximum backup time: 30 days.</li><li>Operation log backup time: 60 days.</li><li>Supports database audit where audit logs can be retained for 15 days and an unlimited number of rules which can be configured.</li></td>
</tr>
<tr>
<td>Standard Edition (one primary and two replicas)</td>
<td>Each shard provides a high-availability architecture based on primary/replica multi-site active-active deployment.</td>
<td>Three nodes: one primary node and two replica nodes</td>
</tr>
<tr>
<td>Finance Edition (one primary and one replica)</td>
<td>Each shard provides a high-availability architecture based on primary/replica active-active deployment.</td>
<td>Two nodes: one primary node and one replica node</td>
<td  rowspan = "2"><li>Supports other deployment schemes. To use other schemes, please contact your Tencent Cloud sale rep.</li><li>Supports read-only replicas and implements intelligent load scheduling for read-only replicas.</li><li>Automatic node failover.</li><li>Default sampling granularity for monitoring: once every 1 minute.</li><li>Maximum backup time: 3,650 days. You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li><li>Operation log backup time: 60 days by default (1 year for archive storage).</li><li>Supports database audit where audit logs can be retained for 15 days.</li><li>Provides assistance for regulatory compliance.</li></td>
</tr>
<tr>
<td>Finance Edition (one primary and two replicas)</td>
<td>Each shard provides a high-availability architecture based on primary/replica multi-site active-active deployment.</td>
<td>Three nodes: one primary node and two replica nodes</td>
</tr>
</tbody></table>
