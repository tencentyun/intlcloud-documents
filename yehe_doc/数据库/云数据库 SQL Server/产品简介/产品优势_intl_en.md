## Official license
Licensed by Microsoft, TencentDB for SQL Server continuously provides you with the latest features, helping you avoid the risks of using unauthorized software and enhancing the trustworthiness of your business in competitive markets.

## High stability and reliability
TencentDB for SQL Server delivers a 99.9996% data reliability and 99.95% service availability. Its primary/replica two-node database architecture allows for switching from a faulty instance to a healthy one in a matter of seconds and enables automatic backup, so the database can be restored to a previous time point through rollback. 

## Best-in-class performance
TencentDB for SQL Server uses enterprise-grade PCI-E SSDs to deliver an industry-leading I/O throughput, outperforming self-built databases and supporting commercial-grade high-volume concurrent business requests.

## Ease of management
Various management tasks can be finished with ease in the Tencent Cloud console or SQL Server Management Studio (SSMS), such as database management, permission configuration, and monitoring and alarming. This eliminates your concerns over database installation and Ops.

## Performance monitoring
Dozens of key metrics can be viewed in the console, such as the number of connections and requests, disk I/O, and buffer hit rate, helping you comprehensively monitor database conditions and accurately understand the database load and system health.

## System alarming
User-defined resource threshold alarms are supported to help you discover database exceptions timely and resolve potential system problems quickly.

## TencentDB for SQL Server's strengths over self-built SQL Server
<table>
<thead><tr><th>Feature</th><th>TencentDB for SQL Server</th><th>Self-Built SQL Server</th></tr></thead>
<tbody>
<tr>
<td>Service availability</td><td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/238/3252" target="_blank">Service Level Agreement</a>.</td><td>You have to guarantee the service availability and set up primary/replica replication and RAID capabilities on your own.</td></tr>
<tr>
<td>System security</td><td>Anti-DDoS is supported, and various database security vulnerabilities are fixed in time. The data security meets all mainstream national and international security standards.</td><td>You have to deploy security services and fix vulnerabilities on your own at high costs. Security compliance is not guaranteed, and the security requirements cannot be quickly met.</td></tr>
<tr>
<td>Database performance</td><td>High-performance devices with a TPM of up to 4.5 million are used. For more information, see <a href="https://intl.cloud.tencent.com/document/product/238/32561" target="_blank">Performance Test Report</a>.</td><td>General devices without optimization and fine-tuning are used.</td></tr>
<tr>
<td>Software and hardware investment</td><td>No hardware or software investment is required, and the service is pay-as-you-go.</td><td>Database servers are costly.</td></tr>
<tr>
<td>System hosting</td><td>There are no hosting fees.</td><td>The hosting fees are high.</td></tr>
<tr>
<td>Deployment and scaling</td><td>The out-of-the-box service can be quickly deployed and elastically scaled.</td><td>You have to purchase hardware devices, host them in data centers, and deploy them on your own. You also have to solve stability problems and set up many supporting modules and management tools, which require heavy investments in technology and take a long period of time.</td></tr>
<tr>
<td>Resource utilization</td><td>The service is billed by the actual usage and supports elastic scaling to ensure a high resource utilization.</td><td>You have to consider traffic spikes, and the resource utilization is low.</td></tr>
<tr>
<td>Data disaster recovery</td><td>Primary/replica replication and backup are configured by default. Both intra-region and cross-region disaster recovery schemes are supported, such as multi-AZ deployment and cross-region backup.
</td><td>You have to find the backup storage space and regularly verify whether backups can be restored, which cost more money and time.</td></tr>
<tr>
<td>Control and management services</td><td>Comprehensive cloud-based instance lifecycle management capabilities are available for various objects, including monitoring and alarming, backup and restoration, instance, database, account, network, parameter, and log.</td><td>You have to implement all control and management capabilities on your own.</td></tr>
<tr>
<td>Procurement costs</td><td>Instances are priced transparently and even more cost-effective than CVM.</td><td>In addition to instances, you also have to set up disaster recovery, monitoring, and management systems on your own at totally uncontrollable costs.</td></tr>
<tr>
<td>License</td><td>Official licenses from Microsoft continuously provide you with the latest features, eliminating your need to purchase additional licenses.</td><td>Pirated services lead to legal risks, while official licenses are expensive.</td></tr>
<tr>
<td>Ops costs</td><td>Tencent Cloud provides a professional team to guarantee the service quality for key accounts 24/7, eliminating your need to manually perform Ops.</td><td>You have to hire dedicated DBAs for database maintenance, which incurs high labor costs.</td></tr>
</tbody></table>

## TencentDB for SQL Server's high availability/disaster recovery capabilities
TencentDB for SQL Server provides disaster recovery capabilities at different levels, including instance, server, data center, AZ, and region, to ensure the business continuity on healthy systems with the minimum data loss in case of natural disasters, device failures, and maloperations. Backup is the basis of all disaster recovery systems and the last line of defense in the high data availability architecture. TencentDB for SQL Server features rich backup capabilities, ensuring that the data can be restored quickly even after a total system crash to guarantee the business continuity as much as possible.

TencentDB for SQL Server provides instances in various architectures with guaranteed high availability:
- **Two-node (formerly high-availability/cluster edition) instance**
 - SQL Server 2008 R2, 2012, 2014, 2016 Enterprise/Standard: The primary/replica architecture of a two-node instance consists of one primary database and one mirror database deployed across racks/AZs and supports automatic HA switch within seconds.
 - SQL Server 2017, 2019 Enterprise/Standard: The primary/replica architecture of a two-node instance adopts the Always On technology to build a cross-racks/AZs SQL Server cluster architecture that features high performance, high availability, high reliability, and easy maintenance and implements automatic HA switch within seconds.
- **Single-node (formerly basic edition) instance**
The underlying layer is deployed in a CVM instance, storage and computing are separated, and data is stored in three copies in premium cloud disk to avoid data loss. In extreme cases where an instance fails, a new instance will be started to automatically restore the data from data and log backups. The specific restoration time is subject to the data volume. The servers of two TencentDB instances are usually on the same physical machine.

For intra-region disaster recovery, TencentDB for SQL Server provides multi-AZ deployment capabilities. Different AZs in the same region are interconnected over the private network, and failures can be isolated between AZs. For instances in the primary/replica two-node architecture, the primary and replica instances can be deployed in different AZs in the same region (for example, one primary instance in the primary AZ and one replica instance in the replica AZ). This improves the business continuity and guarantees the data availability in case of instance failures or AZ disconnections. You can also manually switch between the primary and replica instances in the console to verify the business robustness. Switches within the same AZ and between different AZs are imperceptible to the application.

For remote disaster recovery, cross-region backup capabilities are offered to store backup files in another region. You can set the cross-region backup retention period and multiple backup regions. After a cross-region backup policy is enabled, the instance backup files will be automatically stored in the target region. In this way, if an instance in a region fails, you can restore its backup files in the remote region to a new instance there for guaranteed business continuity. You can also create a cross-region cluster through a cross-region read-only instance, sync data between the primary and read-only instance, switch your business to a remote read-only instance if the region of the primary instance fails. By doing so, you can implement the high availability of database restoration and meet the requirements for data availability and security, remote backup and restoration, remote disaster recovery, long-term data archive, and regulation compliance.

In addition, TencentDB for SQL Server also has rich backup capabilities to guarantee the data security and prevent data loss or corruption. Specifically, you can configure automatic backup, manual backup, data backup, log backup, backup file format (unarchived files or archive file), instance backup, and multi-database backup. You can also customize the backup policy, backup retention period (7–1,830 days), and backup cycle.

Moreover, TencentDB for SQL Server comes with comprehensive disaster recovery capabilities at both the data and business management layers. Cross-region disaster recovery for databases is meaningful only if the business also features cross-region disaster recovery. However, cross-region distributed deployment of the business inevitably causes the split-brain problem. At the business management layer, the business is deployed in three AZs (two intra-region AZs and one remote AZ) to ensure the business continuity. Before an actual failover occurs, the system will always check whether the database sync status (database sync system table) is normal to avoid faulty failover.


