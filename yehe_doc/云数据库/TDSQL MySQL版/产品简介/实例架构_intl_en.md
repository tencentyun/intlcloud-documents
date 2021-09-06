>!The database audit feature is being upgraded, during which new instances won't support this feature. But it will be available again very soon.

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
<td>Standard Edition (one source and one replica)</td>
<td>Each shard provides a high-availability architecture based on source/replica active-active deployment</td>
<td>Two nodes: one source node and one replica node</td>
<td rowspan = "2"><li>Supports real-only replica</li><li>Automatic node failover</li><li>Default sampling granularity for monitoring: once every 5 minutes</li><li>Maximum backup time: 7 days</li><li>Operation log backup time: 7 days</li><li>Supports database audit where audit logs can be retained for 15 days and an unlimited number of rules can be configured</li></td>
</tr>
<tr>
<td>Standard Edition (one source and two replicas)</td>
<td>Each shard provides a high-availability architecture based on source/replica multi-site active-active deployment</td>
<td>Three nodes: one source node and two replica nodes</td>
</tr>
</tbody></table>

