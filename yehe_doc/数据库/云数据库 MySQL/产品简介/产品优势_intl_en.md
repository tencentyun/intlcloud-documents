
>?The strengths described in this document are exclusive to dual-node and three-node TencentDB for MySQL instances.

## Cost Effectiveness and Ease of Use
- **Read/write separation is supported**
Read-only replicas can be mounted to TencentDB for MySQL. One-source-multiple-replica architecture allows you to respond to massive requests. RO group with load balancing feature is supported to greatly optimize the pressure distribution among read-only replicas.

- **Powerful hardware ensures high performance**
NVMe SSD features high IO performance, ensuring smooth reads and writes.
A maximum of 240,000 QPS and a maximum storage space of 6 TB are supported for an instance.

## High Security
- **Protection against DDoS attacks**
When your business suffers a DDoS attack, this feature can help you resist various attack traffic to ensure normal operation.

- **Protection against database attacks**
Effectively defend against database attacks like SQL injection and brute force attacks.

## High Reliability
Data is stored online in a source-replica architecture to ensure security. Moreover, it can be backed up and stored for an extended period of time, allowing for data recovery in the event of a database disaster.

- **Data encryption**
Transparent data encryption (TDE) feature guarantees the security of real-time data and backup data.

- **Database audit**
Financial-grade data audit feature helps prevent core data theft, trace non-compliant operations, and locate malicious pulls.

## High Availability
- **Real-time hot backup**
The dual-server hot backup mechanism supports lossless restoration of data from the last 7–1830 days based on data backup and log backup (binlog). Such backups can be retained for 7–1830 days.

- **Automatic disaster recovery**
Automatic failure detection and failover are supported. Users are not aware of source-replica switchover or failover.

## Advantages over Self-built Databases
- **Easy management of massive databases**
Databases can be managed via command line or console. Batch database management, permission setting, and SQL import are supported. 

- **Data import and backup rollback**
Multiple data import methods are provided for initialization. Data is backed up automatically on a daily basis. TencentDB allows data to be rolled back to any point in time within the retention period based on backup files.

- **Professional monitoring and alarm**
You can monitor resources from multiple dimensions and customize alarming thresholds for them. You can also download reports about slow query analysis and SQL running.

- **A variety of access methods**
Access to the public network and VPC is supported. You can connect TencentDB instances to your IDC, a private cloud, or other computing resources for deployment in a hybrid cloud conveniently.
