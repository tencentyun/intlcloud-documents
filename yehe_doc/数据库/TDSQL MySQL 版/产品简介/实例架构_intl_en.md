
## InnoDB engine
>!As the database audit feature is being refactored and upgraded, it is not available for newly purchased instances during this period.

<table>
<thead><tr><th width="22%">Instance Architecture</th><th>Definition</th><th>Node</th><th>Feature</th></tr></thead>
<tbody><tr>
<td>Standard Edition (one source and one replica)</td>
<td>Each shard provides a high-availability architecture based on source/replica active-active deployment.</td>
<td>Two nodes: One source node and one replica node</td>
<td rowspan = "2"><li>Supports read-only replicas.</li><dx-alert infotype="explain" title="Note">In the 1-source-1-replica architecture, the read-only replica feature can only be used for low-load read-only tasks. Avoid high-load tasks such as large transactions, as they affect the backup tasks and availability of the replica server.</dx-alert><li>Automatic node failover.</li><li>Default sampling granularity for monitoring: Once every 5 minutes.</li><li>Maximum backup time: 7 days.</li><li>Operation log backup time: 7 days.</li><li>Supports database audit where audit logs can be retained for 15 days and an unlimited number of rules which can be configured.</li></td></tr>
<tr>
<td>Standard Edition (one source and two replicas)</td>
<td>Each shard provides a high-availability architecture based on source/replica multi-site active-active deployment.</td>
<td>Three nodes: One source node and two replica nodes</td></tr>
<tr>
<td>Finance Edition (one source and one replica)</td>
<td>Each shard provides a high-availability architecture based on source/replica active-active deployment.</td>
<td>Two nodes: One source node and one replica node</td>
<td  rowspan = "2"><li>Supports other deployment schemes. To use other schemes, contact your Tencent Cloud sale rep.</li><li>Supports read-only replicas and implements intelligent load scheduling for read-only replicas.</li><li>Automatic node failover.</li><li>Default sampling granularity for monitoring: Once every 1 minute.</li><li>Maximum backup time: 3,650 days. You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li><li>Operation log backup time: 60 days by default (1 year for archive storage).</li><li>Supports database audit where audit logs can be retained for 15 days.</li><li>Provides assistance for regulatory compliance.</li></td></tr>
<tr>
<td>Finance Edition (one source and two replicas)</td>
<td>Each shard provides a high-availability architecture based on source/replica multi-site active-active deployment.</td>
<td>Three nodes: One source node and two replica nodes</td></tr>
</tbody></table>

## TDStore engine
In the beta test phase, the TDStore engine adopts a high-availability architecture of three nodes: one source node and two replica nodes.

