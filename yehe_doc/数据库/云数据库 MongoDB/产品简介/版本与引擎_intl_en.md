This document describes the version and storage engine information of TencentDB for MongoDB to help you select appropriate options.

## Versions and Storage Engines
TencentDB for MongoDB supports WiredTiger and Rocks storage engines.

### WiredTiger
With a typical Btree structure, WiredTiger greatly outperforms MMAPv1, MongoDB's legacy storage engine. It provides concurrency control and compression mechanisms at different granularities, significantly reducing the storage costs. It offers the optimal performance and storage efficiency for different types of applications. WiredTiger is the default storage engine in MongoDB 3.2.

### Rocks
Rocks organizes data based on the log-structured merge-tree (LSM tree) structure and specifically optimizes data write capabilities, which guarantee constantly efficient data writes and make it suitable for scenarios involving more writes but fewer reads. It is supported by MongoDB 3.2 only.

| Version    | Storage Engine                |
| ------- | ----------------------- |
| 3.2 | <li>WiredTiger<li>Rocks</li> |
| 3.6 | WiredTiger              |
| 4.0 | WiredTiger              |
| 4.2 | WiredTiger              |
| 4.4 | WiredTiger              |

## Version Description
<table width="100">
<thead>
<tr><th width="15%">Feature Description</th><th width="10%">Subfeature</th><th width="15%">v3.2</th><th width="15%">v3.6</th><th width="15%">v4.0</th><th width="15%">v4.2</th><th width="15%">v4.4</th>    </tr></thead>
<tbody>
<tr>
<td rowspan="4">Network</td>
<td>Classic network</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>    
</tr>
<tr>
<td>VPC</td>
<td>Supported</td>
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
<td>Supported</td>     
</tr>       
 <tr>
<td>Network change</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>      
</tr>        
<tr>
<td rowspan="4">Sale</td>
<tr>
<td>Pay-as-You-Go</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>  
<tr>
<td>Message subscription and notification</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>       
<td rowspan="8">Elasticity</td>
<td>Mongod configuration adjustment</td>
<td>Supported</td>
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
<td>Supported</td>
<td>Supported</td>     
</tr>
<tr>
<td>Adjustment of node quantity per shard</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>     
</tr>
<tr>
<td>Shard quantity adjustment</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>     
</tr>
<tr>
<td>Mongos access address</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>        
<tr>
<td>Mongos node quantity adjustment (sharded cluster)</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>
<td>Secondary node promotion to primary node</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>
<td>Oplog capacity adjustment</td>
<td>Supported</td>    
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>     
<tr>       
<td rowspan="13">Instance operations</td>
<td>Instance list</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Batch instance restart</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Switch to another project</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Password resetting</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Version upgrade</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>    
</tr>       
<tr>
<td>Maintenance time modification</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr> 
<tr>
<td>Read-only instance</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr> 
<tr>
<td>Disaster recovery instance</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>
<td>Multi-AZ deployment</td>
<td>Supported</td>
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
<td>Supported</td>   
</tr>          
<tr>
<td>Data comparison</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Monitoring data export</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>       
<tr>       
<td rowspan="8">Backup and rollback</td>
<td>Backup list</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Automatic backup</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>
<td>Instance clone</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>
<td>Collection rollback (replica set)</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>
<td>Collection rollback (sharded cluster)</td>
<td>Not supported</td>
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
<td>Supported</td>    
</tr>
<tr>       
<td rowspan="7">Database management</td>
<td>Create an account</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr> 
<td>Account permission configuration</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr> 
<td>Slow log request management</td>
<td>Supported</td>
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
<td>Supported</td>
</tr>
 <tr> 
<td>Connection management</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr> 
 <tr> 
<td>Filter by time</td>
<td>Supported</td>
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
<td>Supported</td>     
</tr> 
 <tr> 
<td>Task details display</td>
<td>Supported</td>
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
<td>Supported</td>
<td>Supported</td>    
</tr> 
<tr> 
<td>Audit log</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr>       
<td rowspan="4">Recycle bin</td>
<td>Instance list in recycle bin</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr> 
<td>Batch instance restoration</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>       
<td rowspan="6">Migration</td>
<td>Migration over public network</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>       
<tr> 
<td>Migration over Direct Connect</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr> 
<td>TencentDB migration</td>
<td>Supported</td>
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
<td>Supported</td>    
</tr>
<tr>       
<td rowspan="9">Performance optimization</td>
<td>Exception diagnosis</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr> 
<td>Performance trends monitoring</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>    
</tr>
<tr><td>Slow query analysis</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Space analysis</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>MongoStatus</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>MongoTop</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Real-time session</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Index recommendation</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>SQL throttling</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>   
</tbody></table>

## Minor Version Description

### WiredTiger storage engine on v4.4

| Minor Version      | New Feature, Optimization, or Fix                               |
| ---------- | ------------------------------ |
| WT.44.13.0  | Supported MongoDB 4.4.                                          |



### WiredTiger storage engine on v4.2

| Minor Version      | New Feature, Optimization, or Fix                               |
| ----------- | ------------------------------------------------------------ |
| WT.42.11.15 | <li>Supported auditing database events with custom rules.</li><li>Supported accessing the database through SSL authentication.</li> |
| WT.42.11.14 | Improved the stability of `moveChunk` of the kernel.                                 |
| WT.42.11.13 | Supported using commands to enable the enhanced `changeStream` mode.                     |
| WT.42.11.12 | <li>Fixed the issue where an error was reported when creating and deleting a duplicate database repeatedly.</li><li>Fixed `changeStream` issues.</li> |
| WT.42.11.11 | Fixed the kernel exception during `applyOps`.                               |
| WT.42.11.10 | Optimized the database audit performance.                                           |
| WT.42.11.9  | Supported collection rollback through physical backup to speed up backups.               |
| WT.42.11.8  | Optimized the routing information refresh policy.                                         |
| WT.42.11.7  | Optimized the control logic for adding shards.                                       |
| WT.42.11.6  | Supported DDL operations for `changeStream`.                                      |
| WT.42.11.5  | Optimized kernel parameters to improve the performance.                                         |
| WT.42.11.4  | Blocked high-risk system operations.                                         |
| WT.42.11.3  | Fixed the exception of the `getMore` operation.                                      |
| WT.42.11.2  | Supported the `maxTimeMS` parameter.                                            |
| WT.42.11.1  | Supported the online compact command.                                          |
| WT.42.11.0  | Supported MongoDB 4.2.                                          |

### WiredTiger storage engine on v4.0

| Minor Version      | New Feature, Optimization, or Fix                               |
| ---------- | ------------------------------------------------------------ |
| WT.40.3.34 | <li>Supported auditing database events with custom rules.</li><li>Supported accessing the database through SSL authentication.</li> |
| WT.40.3.33 | <li>Supported speed limit for TTL indexing.</li><li>Supported setting the clearing window for expired TTL data.</li> |
| WT.40.3.32 | <li>Improved the instance stability after collection rollback through physical backup.</li><li>Fixed memory leaks after connection failures.</li> |
| WT.40.3.31 | Supported SQL throttling.                                                  |
| WT.40.3.30 | Supported customizing the slow query threshold.                                     |
| WT.40.3.29 | Optimized the database audit performance.                                           |
| WT.40.3.28 | Optimized the routing information refresh policy for sharded clusters.                                     |
| WT.40.3.27 | Supported collection rollback through physical backup.                             |
| WT.40.3.26 | Optimized the retry lock logic during write conflicts to improve the performance.                             |
| WT.40.3.25 | Optimized user permissions to avoid unauthorized operations.                                   |
| WT.40.3.24 | Prohibited creating LSM engine tables and indexes.                                      |
| WT.40.3.23 | Optimized the logic for adding shards.                                             |
| WT.40.3.22 | Optimized the lock mechanism.                                                   |
| WT.40.3.21 | Optimized the `changeStream` logic.                                         |
| WT.40.3.20 | Optimized the performance.                                                     |
| WT.40.3.19 | Optimized the session logic.                                          |
| WT.40.3.18 | Optimized the secondary database read performance.                                               |
| WT.40.3.17 | Optimized the password-free access logic.                                           |
| WT.40.3.16 | Optimized the monitoring data collection logic.                                             |
| WT.40.3.15 | Supported collections with millions of records.                                             |
| WT.40.3.14 | Optimized the physical backup performance in case of many files.                         |
| WT.40.3.13 | Optimized the mongos connection mechanism.                                           |
| WT.40.3.12 | Optimized the routing information refresh logic and audit performance.                                  |
| WT.40.3.11 | Enhanced `changeStream` capabilities.                                         |
| WT.40.3.10 | Supported the `maxTimeMS` parameter.                                            |
| WT.40.3.9  | Supported mongos overload protection.                                           |
| WT.40.3.8  | Supported database audit.                                               |
| WT.40.3.7  | Optimized the session logic.                                          |
| WT.40.3.6  | Improved the database connection performance and startup performance in case of many files.           |
| WT.40.3.5  | Supported password-free access.                                               |
| WT.40.3.4  | Fixed abnormal bloats of database disk files.                               |
| WT.40.3.3  | Supported IPv6.                                                     |
| WT.40.3.2  | <li>Supported blocking writes to full disks.</li> <li>Supported displaying the client connection information.</li>  |
| WT.40.3.1  | <li>Supported the `superGeo` command.</li>Supported physical backup.</li><li>Added new monitoring metrics.</li> |
| WT.40.3.0  | Released MongoDB 4.0 based on the WiredTiger engine.                      |

### WiredTiger storage engine on v3.6

| Minor Version     | Description                                             |
| ---------- | ---------------------------------------------------- |
| WT.36.8.12 | <li>Optimized the password-free access logic.</li><li>Optimized the display effect of the client list.</li> |
| WT.36.8.11 | Optimized the connection performance.                                       |
| WT.36.8.10 | Optimized the logic of session and cross-node data sync.             |
| WT.36.8.9  | Supported physical backup.                                         |
| WT.36.8.8  | Supported password-free access.                                         |
| WT.36.8.7  | Optimized the mongos connection pool mechanism.                                 |
| WT.36.8.6  | Optimized the connection logic.                                       |
| WT.36.8.5  | Supported IPv6.                                             |
| WT.36.8.4  | Optimized the monitoring data collection logic.                                     |
| WT.36.8.3  | Optimized the disk blocking logic.                                     |
| WT.36.8.2  | Optimized the connection model.                                         |
| WT.36.8.1  | Optimized the security mechanism.                                     |
| WT.36.8.0  | Supported v3.6.                                          |

### WiredTiger storage engine on v3.2

| Minor Version     | Description                                                     |
| ---------- | ------------------------------------------------------------ |
| WT.32.12.9 | Supported setting the maximum timeout period of requests and creating indexes with the instance in the background by default. |
| WT.32.12.8 | Optimized the mongos connection pool mechanism.                               |
| WT.32.12.7 | Supported IPv6 and its parameter configuration.                                           |
| WT.32.12.6 | Optimized kernel connection parameters to improve the performance.                                   |
| WT.32.12.5 | Fixed issues such as occasional kernel exception.                                     |
| WT.32.12.4 | Supported the `superGeoNear` command.                                         |
| WT.32.12.3 | Optimized kernel parameters to improve the performance.                                         |
| WT.32.12.2 | Supported adjusting the oplog capacity.                                            |
| WT.32.12.1 | Supported dynamically adjusting the number of connections.                                           |
| WT.32.12.0 | Supported the WiredTiger engine of MongoDB 3.2.                            |

### Rocks storage engine on v3.2

| Minor Version        | Description                               |
| ------------- | -------------------------------------- |
| ROCKS.32.12.3 | Optimized connection parameters and performance.                     |
| ROCKS.32.12.2 | Optimized the secondary database read performance.                         |
| ROCKS.32.12.1 | Supported read requests from secondary databases and optimized snapshot expiration parameters. |
| ROCKS.32.12.0 | Supported the Rocks storage engine.                      |

