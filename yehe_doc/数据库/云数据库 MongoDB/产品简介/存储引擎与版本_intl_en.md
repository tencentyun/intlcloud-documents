This document describes the storage engines and version information of TencentDB for MongoDB to help you select appropriate options.

## Storage Engine
TencentDB for MongoDB supports WiredTiger and Rocks storage engines.

### WiredTiger
With a typical Btree structure, WiredTiger greatly outperforms MMAPv1, MongoDB's legacy storage engine. It provides concurrency control and compression mechanisms at different granularities, significantly reducing the storage costs. It offers the optimal performance and storage efficiency for different types of applications. MongoDB 3.2 uses WiredTiger as the default storage engine.

### Rocks
Rocks organizes data based on the log-structured merge-tree (LSM tree) structure and specifically optimizes data write capabilities, which guarantee constantly efficient data writes and make it suitable for scenarios involving more writes but fewer reads. It is supported by MongoDB 3.2 only.

| Version    | Storage Engine                |
| ------- | ----------------------- |
| 3.2 | <li>WiredTiger<li>Rocks</li> |
| 3.6 | WiredTiger              |
| 4.0 | WiredTiger              |
| 4.2 | WiredTiger              |

## Version Description
<table width="100">
<thead>
<tr>
<th width="15%">Feature</th>
<th width="25%">Subfeature</th>
<th width="15%">3.2</th>
<th width="15%">3.6</th>
<th width="15%">4.0</th>
<th width="15%">4.2</th>
</tr></thead>
<tbody>
<tr>
<td rowspan="4">Network</td>
<td>Classic network</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>VPC</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Security group</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>       
 <tr>
<td>Network change</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>        
 <tr>
<td rowspan="5">Sale</td>
<tr>
<td>Pay-as-You-Go</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Batch renewal</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
<tr>
<td>Pay-as-You-Go instance termination</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>  
<tr>
<td>Message subscription and notification</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>       
<td rowspan="4">Elasticity</td>
<td>Configuration adjustment</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Node quantity adjustment</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Adjustment of node quantity per shard</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Shard quantity adjustment</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>       
<td rowspan="10">Instance operation</td>
<td>Instance list</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>       
<tr>
<td>Restart an instance</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Batch instance restart</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Instance termination</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Switch to another project</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Tag management</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Password resetting</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Unauthorized access</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Version upgrade</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>       
<tr>
<td>Maintenance time modification</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
<tr>       
<td rowspan="5">System monitoring</td>
<td>Monitoring metric list</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>          
<tr>
<td>Data comparison</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Alarm rule configuration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Monitoring data export</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Multi-Instance comparison and monitoring</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>       
<tr>       
<td rowspan="8">Backup and rollback</td>
<td>Backup list</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Manual backup</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Automatic backup</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
<tr>
<td>Backup file download</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Instance clone</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Database table rollback (replica set)</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Database table rollback (sharded cluster)</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Automatic backup policy configuration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>       
<td rowspan="7">Database management</td>
<td>Create an account</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Account password change</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Account permission configuration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Slow log query</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Slow log request management</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
 <tr> 
<td>Slow log download</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
 <tr> 
<td>Connection management</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>       
<td rowspan="4">Task management</td>
<td>List data loading</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
 <tr> 
<td>Filter by time</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
 <tr> 
<td>Filter by instance name</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
 <tr> 
<td>Task details display</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>       
<td rowspan="2">Database audit</td>
<td>Instance audit</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr> 
 <tr> 
<td>Audit log</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>       
<td rowspan="4">Recycle bin</td>
<td>Instance list in recycle bin</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Instance restoration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Batch instance restoration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Instance elimination</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>       
<td rowspan="6">Migration</td>
<td>Migration over public network</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Self-Build on CVM</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>       
<tr> 
<td>Migration over Direct Connect</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Migration over VPN</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>TencentDB migration</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr> 
<td>Migration over CCN</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr> 
</tbody></table>


