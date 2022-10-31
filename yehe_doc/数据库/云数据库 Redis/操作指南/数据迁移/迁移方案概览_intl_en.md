With the help of [DTS](https://intl.cloud.tencent.com/document/product/571) as well as redis-sync, redis-dump, and redis-restore tools in the [redis-port](https://intl.cloud.tencent.com/document/product/239/31940) migration toolkit, TencentDB for Redis offers a variety of data migration schemes for diverse business scenarios. 

## Migration Tools

- [DTS](https://intl.cloud.tencent.com/document/product/239/31941): It helps migrate your database to the cloud without interrupting your business. In its full + incremental data migration mode, historical data in the source database written before migration and incremental data written during migration can be migrated together.
- [redis-sync](https://intl.cloud.tencent.com/document/product/239/31940): It supports data migration between Redis instances. It is simulated as a replication node to sync data from the source instance and translate the replicated data into write commands to update the target instance. 
- [redis-dump and redis-restore](https://intl.cloud.tencent.com/document/product/239/31940): redis-dump can be used to back up Redis data into RDB files in an offline environment, and then redis-restore can be used to import the RDB files into the specified Redis instance. 

## Migration Solutions

<table class="table-striped">
<tbody>
<thead><tr><th>Migration Scenario</th><th>Category</th><th>Migration Tool</th><th>Access Type</th><th>Description</th></tr></thead>
<tr>
<td rowspan="6"><b>Migration from self-built Redis to TencentDB for Redis</b></td>
<td rowspan="3">Migration from IDC-based self-built Redis to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>The following three access types are supported:
<ul><li>Direct Connect: The source database can be interconnected with VPCs through direct connect. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/216/7557">Getting Started</a></li>
  <li>VPN Access: The source database can be interconnected with VPCs through VPN connection. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/1037">VPN Connections</a>
  <li>Intranet (only suitable for Tencent's internal businesses): You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></ul></td>
<td>
<ul><li>The migration is online, with full + incremental data sync supported.</li>
  <li>Supported source Redis versions are 2.8, 3.0, 4.0, 5.0, and 6.0, and supported target Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li>   
  <li>Supported architectures include single-node, Redis cluster, Twemproxy, and Sentinel.</li></ul></td></tr>	
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">Redis-sync</a></td>
<td>The following two access types are supported:
<ul><li>Public Network: The source database can be accessed through a public IP.</li><li>Intranet: You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></ul></td>
<td>
<ul><li>The migration is online, with full + incremental data sync supported.</li>
 <li>The source Redis database must allow the `SYNC` or `PSYNC` command.</li>
 <li>Supported source Redis versions are 2.8, 3.0, and 4.0, and supported target Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></ul></td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">redis-dump and redis-restore</a></td><td>Offline (the source and target databases don't interconnect over the network).</td>
<td>
<li>The migration is offline, with only full data sync supported. Business downtime will be caused.</li>
<li>Supported source Redis versions are 2.8, 3.0, and 4.0, and supported target Redis versions are 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr>
<tr>
<td rowspan="3">Migration from CVM-based self-built Redis to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>Self-Built on CVM: The source database is deployed in a <a href="https://intl.cloud.tencent.com/document/product/213">CVM</a> instance.</td><td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported source Redis versions are 2.8, 3.0, 4.0, 5.0, and 6.0, and supported target Redis versions are 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li>
<li>Supported architectures include single-node, Redis cluster, Twemproxy, and Sentinel.</li></td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">Redis-sync</a></td>
<td>VPC: The source database can be accessed via <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a></td><td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>The source Redis database must allow the `SYNC` or `PSYNC` command.</li>
<li>Supported source Redis versions are 2.8, 3.0, and 4.0, and supported target Redis versions are 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">redis-dump and redis-restore</a></td>
<td>Offline (the source and target databases don't interconnect over the network).</td>
<td>
<li>The migration is offline, with only full data sync supported. Business downtime will be caused.</li>
<li>Supported source Redis versions are 2.8, 3.0, and 4.0, and supported target Redis versions are 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr>
<tr>
<td><b>Migration from TencentDB for Redis to self-built Redis</b></td>
<td>Migration from TencentDB for Redis to self-built Redis (migration off the cloud and multi-cloud sync)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>The following five access types are supported:
<li>Public Network: The source database can be accessed through a public IP.</li>
<li>Self-Build on CVM: The source database is deployed in a CVM instance.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216/7557">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003/31985">CCN</a></li>
</td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></td><td>
<li>Supported target instance types include single-node, Redis cluster, and proxy cluster (which can be deployed by using the proxy provided by Tencent Cloud).</li></td></tr>    
<tr>
<td rowspan="6"><b>Migration between TencentDB for Redis instances</b></td>
<td>Migration between TencentDB for Redis instances in different regions</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>CCN: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1003/31985">CCN</a></td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr>
<tr>
<td>Migration between TencentDB for Redis instances in the same region</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>Database: The source database is a TencentDB database.</td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li>
<li>This scheme is suitable for large-shard cluster architecture upgrade as it can shorten the downtime.</li></td></tr>
<tr>
<td>Migration between TencentDB for Redis instances on different versions</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>
<li>Database: The source database is a TencentDB database.</li>
<li>VPC: The source database can be accessed through <a href="https://intl.cloud.tencent.com/document/product/215">VPC</a></li></td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/239/32546">Version Upgrade with DTS</a>.</li></td></tr>
<tr>
<td>Migration across Tencent Cloud accounts</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>Database: The source database is a TencentDB database.</td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li><li>Supported Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li>
<li>You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></td></tr>
<tr>
<td>Migration from Tencent Cloud standard architecture to cluster architecture</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>Database: The source database is a TencentDB database.</td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li>
<li>Check the command compatibility as instructed in <a href="https://intl.cloud.tencent.com/document/product/239/37594">Check on Migration from Standard Architecture to Cluster Architecture</a> in advance to avoid service execution errors after the upgrade.</li></td></tr>
<tr>
<td>Migration from legacy TencentDB for Redis Cluster Edition instance (purchased before January 1, 2018)</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">redis-restore</a></td><td>Offline (VPC)</td>
<td>
<li>Only full data sync is supported. Business downtime will be caused.</li>
<li>For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/239/31942">Migration Guide for Legacy Cluster Edition</a>.</li></td></tr> 
<tr>
<td rowspan="2"><b>Migration from another cloud to TencentDB for Redis</b></td>
<td rowspan="2">Migration from Redis in another cloud to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31941"> DTS (recommended)</a></td>
<td>The following three access types are supported:
<li>Public Network: The source database can be accessed through a public IP.</li>
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216/7557">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/1037">VPN Connections</a></li></td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>The third-party cloud vendor must allow the `SYNC` or `PSYNC` command.</li>
<li>Supported source Redis versions are 2.8, 3.0, 4.0, 5.0, and 6.0, and supported target Redis versions are 2.8, 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr> 
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940">redis-dump and redis-restore</a></td>
<td>Offline (the source and target databases don't interconnect over the network).</td>
<td>
<li>The migration is offline, with only full data sync supported. Business downtime will be caused.</li>
<li>Supported source Redis versions are 2.8, 3.0, and 4.0, and supported target Redis versions are 4.0, 5.0, and 6.0. The target version must be later than or equal to the source version.</li></td></tr>
<tr>
<td rowspan="6"><b>Migration from another type of database to TencentDB for Redis</b></td>
<td>Migration from SSDB to TencentDB for Redis</td>
<td><a href="https://cloud.tencent.com/document/product/239/76626"> Siphon </a></td>
<td>The following four access types are supported:
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216/7557">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/1037">VPN Connection</a>.</li>
<li>VPC: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/215/31891">VPC</a></li>
<li>Intranet: You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></td><td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>All SSDB kernel versions are supported.</li></td></tr>
<tr>
<td>Migration from Pika to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/48547"> pika-migrate </a></td><td>support the following four access types:
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216/7557">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://www.tencentcloud.com/document/product/1037">VPN Connections</a>.</li>
<li>VPC: The source database can be accessed through <a href="https://intl.cloud.tencent.com/document/product/215/31891">VPC</a></li>
<li>Intranet: You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></td><td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>Supported Pika versions are 2.2, 2.3, 3.0, 3.1, and 3.2.</li>
<li>Only standalone single-database Pika instances are supported.</li></td></tr>
<tr>
<td>Migration from Codis to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/48547"> DTS </a></td><td>support the following four access types:
<li>Direct Connect: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/216/7557">Direct Connect</a>.</li>
<li>VPN Access: The source database can be interconnected with VPCs through <a href="https://intl.cloud.tencent.com/document/product/1037">VPN Connections</a>.</li>
<li>VPN: The source database can be accessed through <a href="https://intl.cloud.tencent.com/document/product/215/31891">VPC</a></li>
<li>Intranet: You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</li></td>
<td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>The source node must allow the `SYNC` or `PSYNC` command.</li>
<li>All versions are supported. For migration of Tencent's internal businesses to the cloud, you need to submit a ticket for application.</li></td></tr>
<tr>
<td>Migration from Tencent istore to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/48547"> DTS </a></td>
<td>Intranet: You need to <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> for application.</td><td>
<li>The migration is online, with full + incremental data sync supported.</li>
<li>The source node must allow the `SYNC` or `PSYNC` command.</li><li>All istore versions are supported.</li></td></tr>
<tr>
<td>Migration from Memcached to TencentDB for Redis</td>
<td>-</td><td>-</td><td>Contact Tencent Cloud to customize a migration scheme.</td></tr>
<tr>
<td>Migration from Tencent Cloud CKV to TencentDB for Redis</td>
<td><a href="https://intl.cloud.tencent.com/document/product/239/31940"> redis-restore </a></td>
<td>Offline (the source and target databases don't interconnect over the network).</td>
<td><li>Only full data sync is supported. Business downtime will be caused.</li>
<li>For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/239/31942">Migration Guide for Legacy Cluster Edition</a>.</li></td></tr>    
</tbody></table>

