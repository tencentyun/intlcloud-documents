This document describes the features and differences of TencentDB for SQL Server editions.

## Edition Features and Differences
<table>
<tr><td rowspan=2>Module</td><td rowspan=2>Feature</th><td>Dual-Server High Availability Edition</td><td>Cluster Edition</td><td>Basic Edition</td></tr>
<tr>
<td>2008 R2 Enterprise<br>2012 Standard/Enterprise<br>2014 Standard/Enterprise<br>2016 Standard/Enterprise<br>2017 Standard/Enterprise<br>2019 Standard/Enterprise</td>
<td>2017 Enterprise<br>2019 Enterprise</td>
<td>2008 R2 Enterprise<br>2012 Enterprise<br>2014 Enterprise<br>2016 Enterprise<br>2017 Enterprise<br>2019 Enterprise</td></tr>
<tr>
<td rowspan=10>Lifecycle</td>
<td>Instance creation</td><td rowspan=11>Supported</td><td rowspan=11>Supported</td><td rowspan=11>Supported</td></tr>
<tr><td>Instance restart</td></tr>
<tr><td>Billing mode change</td></tr>
<tr><td>Instance termination</td></tr>
<tr><td>Read-only instance creation</td></tr>
<tr><td>Publish/Subscribe</td></tr>
<tr><td>Specification upgrade/downgrade</td></tr>
<tr><td>Disk capacity adjustment</td></tr>
<tr><td>Version upgrade</td></tr>
<tr><td>Architecture upgrade</td></tr>
<tr>
<td rowspan=7>Instance attribute</td>
<td>Instance list view</td><td rowspan=7>Supported</td><td rowspan=7>Supported</td><td rowspan=7>Supported</td></tr>
<tr><td>Instance details view</td></tr>
<tr><td>Instance renaming</td></tr>
<tr><td>Instance remarks modifying</td></tr>
<tr><td>Instance tagging</td></tr>
<tr><td>Maintenance time management</td></tr>
<tr><td>Project management</td></tr>
<tr>
<td rowspan=5>Service availability</td>
<td>High availability method</td><td>Mirror HA</td><td>Always On high availability</td><td>Compute node migration + disk snapshot</td></tr>
<tr><td>Cross-AZ disaster recovery</td><td>Supported</td><td>Supported</td><td>Unsupported</td></tr>
<tr><td>Intra-region disaster recovery</td><td>Supported</td><td>Supported</td><td>Unsupported</td></tr>
<tr><td>Read-only instance removal</td><td>Supported</td><td>Supported</td><td>Unsupported</td></tr>
<tr><td>Cross-AZ migration</td><td>Supported</td><td>Supported</td><td>Unsupported</td></tr>
<tr>
<td rowspan=16>Backup and restoration</td>
<td>Full backup</td><td rowspan=15>Supported</td><td rowspan=15>Supported</td><td rowspan=15>Supported</td></tr>
<tr><td>Data backup</td></tr>
<tr><td>Incremental backup</td></tr>
<tr><td>Log backup</td></tr>
<tr><td>Scheduled backup</td></tr>
<tr><td>Manual backup</td></tr>
<tr><td>Archive file</td></tr>
<tr><td>Unarchived files</td></tr>
<tr><td>Instance backup</td></tr>
<tr><td>Multi-database backup</td></tr>
<tr><td>Backup policy customization</td></tr>
<tr><td>Restoration by backup set</td></tr>
<tr><td>Restoration by time point</td></tr>
<tr><td>Restoration by user backup set</td></tr>
<tr><td>Backup download</td></tr>
<td>Backup task execution on replica instance</td><td>Unsupported</td><td>Supported</td><td>Unsupported</td></tr>
<tr>
<td rowspan=5>Monitoring and alarms</td>
<td>Resource monitoring</td><td rowspan=3>Supported</td><td rowspan=3>Supported</td><td >Supported</td></tr>
<tr><td>Engine monitoring</td><td >Supported</td></tr>
<tr><td>Second-level monitoring</td><td >Unsupported (one-minute granularity)</td></tr>
<tr><td>Monitoring policy customization</td><td>Unsupported</td><td>Unsupported</td><td>Supported</td></tr>
<tr><td>Alarm</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan=4>Account management</td>
<td>Account creation and deletion</td><td rowspan=3>Supported</td><td rowspan=3>Supported</td><td rowspan=3>Supported</td></tr>
<tr><td>Read/Write permission separation</td></tr>
<tr><td>Admin account</td></tr>
<tr><td>SA account</td><td>Unsupported</td><td>Unsupported</td><td>Supported</td></tr>
<td rowspan=7>Database management</td>
<td>Database creation</td><td rowspan=7>Supported</td><td rowspan=7>Supported</td><td rowspan=7>Supported</td></tr>
<tr><td>Database deletion</td></tr>
<tr><td>Database cloning</td></tr>
<tr><td>Database authorization</td></tr>
<tr><td>Change data capture (CDC)</td></tr>
<tr><td>Change tracking (CT)</td></tr>
<tr><td>Database shrinking</td>
<tr>
<td rowspan=4>Data security</td>
<td>Security group</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Database audit</td><td rowspan=2>Unsupported currently</td><td rowspan=2>Unsupported currently</td><td rowspan=3>Unsupported</td></tr>
<tr><td>Network encryption</td></tr>
<tr><td>TDE encryption</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan=4>Data channel</td>
<td>Data sync</td><td>Unsupported currently</td><td>Unsupported currently</td><td>Unsupported currently</td></tr>
<tr><td>Homogeneous data migration </td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Heterogeneous data migration</td><td >Unsupported</td><td >Unsupported</td><td rowspan=2>Unsupported</td></tr>
<tr><td>Publish/Subscribe</td><td>Supported</td><td>Supported</td></tr>
<tr>
<td rowspan=3>Log management</td>
<td>Error log</td><td>Unsupported</td><td>Unsupported</td><td>Unsupported</td></tr>
<tr><td>Slow log</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Execution log</td><td>Unsupported</td><td>Unsupported</td><td>Unsupported</td></tr>
<tr>
<td rowspan=3>Parameter management</td>
<td>Parameter update</td><td rowspan=2>Supported</td><td rowspan=2>Supported</td><td rowspan=2>Supported</td></tr>
<tr><td>Parameter history</td></tr>
<tr><td>Parameter template</td><td>Unsupported</td><td>Unsupported</td><td>Unsupported</td></tr>
<tr>
<td rowspan=3>Performance optimization</td>
<td>Expert service</td><td>Supported</td><td>Supported</td><td>Supported</td></tr>
<tr><td>Resource analysis</td><td rowspan=2>Unsupported</td><td rowspan=2>Unsupported</td><td rowspan=2>Unsupported</td></tr>
<tr><td>Engine analysis</td></tr>
<tr>
<td rowspan=3>Network</td>
<td>Classic network</td><td rowspan=2>Supported</td><td rowspan=2>Supported</td><td rowspan=2>Supported</td></tr>
<tr><td>VPC</td></tr>
<tr><td>Public address</td><td>Unsupported</td><td>Unsupported</td><td>Unsupported</td></tr>
</tbody></table>


