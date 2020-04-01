>The strengths described in this document are exclusive to TencentDB for MySQL High-Availability Edition instances.

## Cost Effectiveness and Ease of Use

#### Read/Write separation
Read-only instances can be mounted to MySQL. The one-master-multiple-slave architecture allows you to respond to a multitude of business requests with ease. Load balancing-enabled RO groups can be created, helping evenly distribute the load among read-only instances.

#### Powerful hardware for high performance
NVMe SSD features high IO performance, ensuring smooth reads and writes.
One single instance can sustain up to 240,000 QPS with a maximum storage capacity of 6 TB.

## High Security
#### DDoS protection
This feature helps defend against various DDoS attacks, large and small, to ensure business continuity.

#### Protection against database attacks
Database attacks such as SQL injections and brute force attacks can be blocked efficiently.

## High Reliability
Data is stored online in a master/slave architecture, ensuring high data security. Moreover, backup data can be stored for an extended time period, allowing for data recovery in case of a database disaster.

#### Data encryption
Transparent data encryption (TDE) feature guarantees the security of real-time data and backup data.

#### Database audit
Financial-grade data audit feature helps prevent core data theft, trace non-compliant operations, and locate malicious pulls.


## High Availability
#### Real-Time hot backup
The dual-server hot backup mechanism supports lossless restoration of data from the last 7–732 days based on data backup and log backup (binlog). Such backups can be retained for 7–732 days.

#### Automated disaster recovery
Automated failure detection and failover are supported. Master/slave switch and failover are imperceptible to users.

## Advantages over Self-Built Databases
#### Easy management of massive databases
Databases can be managed via command line or console. Batch database management, permission setting, and SQL import are supported. 

#### Data import, backup, and rollback
Multiple data import methods are provided for initialization. Data is automatically backed up daily and can be rolled back to any point in time in the last 5 days based on backup files.

#### Professional monitoring and alarming
Multidimensional monitoring and alarming based on custom resource thresholds are supported. You can also download slow query analysis reports and complete SQL running reports.

#### Multiple network access methods
Access to the public network and VPC is supported. You can connect TencentDB instances to your IDC, a private cloud, or other computing resources for deployment in a hybrid cloud conveniently.
