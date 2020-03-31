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
<td>Standard Edition (one master and one slave)</td>
<td>Each shard provides a high-availability architecture based on master/slave active-active deployment</td>
<td>Two nodes: one master node and one slave node</td>
<td rowspan = "2"><li>Supports real-only slave</li><li>Automatic node failover</li><li>Default sampling granularity for monitoring: once every 5 minutes</li><li>Maximum backup time: 30 days</li><li>Operation log backup time: 60 days</li><li>Supports database audit where audit logs can be retained for 15 days and an unlimited number of rules can be configured</li></td>
</tr>
<tr>
<td>Standard Edition (one master and two slaves)</td>
<td>Each shard provides a high-availability architecture based on master/slave multi-site active-active deployment</td>
<td>Three nodes: one master node and two slave nodes</td>
</tr>
<tr>
<td>Finance Edition (one master and one slave)</td>
<td>Each shard provides a high-availability architecture based on master/slave multi-site active-active deployment</td>
<td>Two nodes: one master node and one slave node</td>
<td  rowspan = "2"><li>Supports the cage deployment scheme. To use this scheme, please contact your Tencent Cloud sale rep</li><li>Supports read-only slaves and implements intelligent load scheduling for read-only slaves</li><li>Automatic node failover</li><li>Default sampling granularity for monitoring: once every 1 minute</li><li>Maximum backup time: 3,650 days. You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application</li><li>Operation log backup time: 60 days by default (1 year for archive storage)</li><li>Supports database audit where audit logs can be retained for 15 days</li><li>Provides assistance for regulatory compliance</li></td>
</tr>
<tr>
<td>Finance Edition (one master and two slaves)</td>
<td>Each shard provides a high-availability architecture based on master/slave multi-site active-active deployment</td>
<td>Three nodes: one master node and two slave nodes</td>
</tr>
</tbody></table>
