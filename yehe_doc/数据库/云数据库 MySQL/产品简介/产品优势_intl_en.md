## Strengths of Single-Node Instances
### High cost effectiveness
Computing resources start at as low as 3.685 USD/month, greatly reducing the deployment costs.
### Large disks
Up to 30 TB storage space is available, with no limits on disk specification.
### High security
- **Anti-DDoS protection**
When your business suffers a DDoS attack, this feature can help you resist various attack traffic to ensure normal operation.

- **Protection against database attacks**
Effectively defense against such database attacks as SQL injection and brute force attacks.

### High reliability
The system adopts a distributed three-copy storage mechanism and guarantees that data is written in all three copies before returning a response of successful write. If any copy fails, the backend data replication mechanism can quickly create a new copy by using methods such as data migration, ensuring the availability of three data copies at all times and increasing the data reliability.

### Strengths over self-built databases
- **Easy management of massive databases**
Databases can be managed via command line or console. Batch database management, permission setting, and SQL import are supported.

- **Data import and backup rollback**
Multiple data import methods are provided for initialization. Data is backed up automatically on a daily basis. TencentDB allows data to be rolled back to any point in time within the retention period based on backup files.

- **Professional monitoring and alarm**
You can monitor resources from multiple dimensions and customize alarming thresholds for them. You can also download reports about slow query analysis and SQL running.

- **A variety of access methods**
Access to the public network and VPC is supported. You can connect TencentDB instances to your IDC, a private cloud, or other computing resources for deployment in a hybrid cloud conveniently.

## Strengths of Two-Node/Three-Node Instances
### High cost performance
- **Flexible billing modes**
Pay-as-you-go and monthly subscription billing modes are available, so you don't have to invest a lump sum of money in infrastructure construction.

- **Read/Write separation**
Read-only instances can be mounted to TencentDB for MySQL. The one-source-multiple-replica architecture allows you to respond to massive requests. RO group with the load balancing feature is supported to greatly optimize the pressure distribution among read-only instances.

- **Powerful hardware for high performance**
NVMe SSD features high IO performance, ensuring smooth reads and writes.
A single instance can sustain up to 240,000 QPS and 6 TB storage space.

### High security
- **Anti-DDoS protection**
When your business suffers a DDoS attack, this feature can help you resist various attack traffic to ensure normal operation.

- **Protection against database attacks**
Effectively defense against such database attacks as SQL injection and brute force attacks.

### High reliability
Data is stored online in a source-replica architecture to ensure security. Moreover, it can be backed up and stored for an extended period of time, allowing for data recovery in the event of a database disaster.

- **Data encryption**
Transparent data encryption (TDE) feature guarantees the security of real-time data and backup data.

- **Database audit**
Financial-grade data audit feature helps prevent core data theft, trace non-compliant operations, and locate malicious pulls.

### High availability
- **Real-time hot backup**
The dual-server hot backup mechanism supports lossless restoration of data from the last 7–1830 days based on data backup and log backup (binlog). Such backups can be retained for 7–1830 days.

- **Automatic disaster recovery**
Automatic failure detection and failover are supported. Users are not aware of source-replica switchover or failover.

### Strengths over self-built databases
- **Easy management of massive databases**
Databases can be managed via command line or console. Batch database management, permission setting, and SQL import are supported.

- **Data import and backup rollback**
Multiple data import methods are provided for initialization. Data is backed up automatically on a daily basis. TencentDB allows data to be rolled back to any point in time within the retention period based on backup files.

- **Professional monitoring and alarm**
You can monitor resources from multiple dimensions and customize alarming thresholds for them. You can also download reports about slow query analysis and SQL running.

- **A variety of access methods**
Access to the public network and VPC is supported. You can connect TencentDB instances to your IDC, a private cloud, or other computing resources for deployment in a hybrid cloud conveniently.
