>The strengths described in this document are exclusive to TencentDB for MySQL High Availability Edition instances.

## Cost Effectiveness and Ease of Use

#### Read-write separation
Read-only instances can be mounted to MySQL. The one-master-multiple-slave architecture allows you to respond to a multitude of business requests with ease. Load balancing-enabled RO groups can be created, helping evenly distribute the load among read-only instances.

#### Powerful hardware for high performance
NVMe SSD features high IO performance, ensuring smooth reads and writes.
>A single instance can sustain up to 240,000 QPS with a maximum storage space of 6 TB.

## High Security

#### DDoS protection
This feature helps defend against various DDoS attacks, large and small, to ensure business continuity.

#### Protection against database attacks
Database attacks such as SQL injections and brute force attacks can be blocked efficiently.

## High Reliability
Data is stored online in a master-slave architecture, ensuring high data security. Moreover, backup data can be stored for multiple days via the backup mechanism, allowing for data recovery in case of a database disaster.

#### Data encryption
The transparent data encryption (TDE) feature is provided to guarantee the security of real-time data and backup data.

#### Database audit
The finance-grade data audit feature helps prevent core data theft, trace non-compliant operations, and locate malicious pulls.

## High Availability

#### Real-time hot backup
The dual-server hot backup mechanism supports lossless recovery of data from the past 5 days based on binlog. Moreover, dumps of cold backup data from the past 7 days can be created.

#### Automatic disaster recovery
Automatic failure detection and failover are supported. Master/slave switch and failover are imperceptible to users.

## Advantages over Self-built Databases

#### Easy management of massive databases
Instances can be managed using command line or on the web and support batch database management, permission setting, and SQL import.

#### Data import and backup rollback
Multiple data import methods are provided for initialization. Data is automatically backed up daily and can be rolled back to any point in time in the past 5 days based on the backup file.

#### Professional monitoring and alarming
Multi-dimensional monitoring and alarming based on custom resource thresholds are supported. Slow log analysis reports and complete SQL running reports can be downloaded.

#### Multiple network access methods
Access to the public network and VPC is supported, enabling you to connect TencentDB instances to your IDC, a private cloud, or other computing resources and apply them in a hybrid cloud conveniently.
