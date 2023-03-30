This document describes the common concepts of TencentDB for SQL Server to help you better understand and use it.

- **Database instance**
A database instance is a database server. One or multiple databases can be created in a database instance, and one or multiple tables can be created in a database.
- **Primary instance and replica instance**
For High Availability or Cluster Edition instances, the node that your business accesses is called primary instance, and the data of the primary instance is synced to another node called replica instance in real time.
You can access only the primary instance, while the replica instance exists only as a backup and does not provide business access. When the primary instance fails, a primary-replica switch imperceptible to applications will be performed, and only a momentary disconnection may occur during the switch.
- **Read-only instance**
A read-only instance elastically expands the read capacity and mitigates the database pressures. In scenarios where there are many read requests but only few write requests, a single instance may not be able to handle the load of read requests, which even may affect the business. In this case, you can create one or multiple read-only instances and use them to sustain high numbers of database reads and increase the application throughput.
- **Tencent Cloud console**
Tencent Cloud console consists of web-based UIs.
- **Region**
The geographic location of a physical IDC. In general, a TencentDB for SQL Server instance and a CVM instance should be in the same region to achieve the best access performance.
- **Availability zone (AZ)**
A physical location with independent power supply and network resources within a region. There are no substantial differences between different AZs in the same region.
- **Multi-AZ**
A physical location created by combining multiple AZs in the same region.
- **RO group**
A group of read-only instances.
- **Billing mode**
The billing mode of an instance resource, which is pay-as-you-go.
- **Pay-as-you-go**
A postpaid billing mode, where you can apply for resources for on-demand use and will be charged based on the actual usage upon settlement.
- **Instance type**
Single-node (formerly Basic Edition) and two-node (formerly High Availability/Cluster Edition) instances in terms of deployment architecture.
- **Single-node (formerly Basic Edition)**
A TencentDB for SQL Server single-node (formerly Basic Edition) instance is also called a standalone instance. It has only one database node, separates computing and storage, and is very cost-effective.
- **Two-node (formerly High Availability/Cluster Edition)**
A two-node instance consists of a primary instance and a replica instance. When the former fails and cannot be accessed, the system will automatically switch to the latter.
A 2008 R2 Enterprise, 2012 Enterprise, or 2016 Enterprise two-node instance consists of one primary database and one mirror database deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.
 A 2017 Enterprise or 2019 Enterprise two-node instance adopts the Always On architecture, including one primary and one replica deployed across racks/AZs. Each database corresponds to a monitoring agent that monitors the database through heartbeat in real time.
- **Engine versions**
Compatible database versions. Currently, the following versions are supported: 2008 R2 Enterprise, 2012 Enterprise, 2016 Enterprise, 2017 Enterprise, and 2019 Enterprise.
- **Specification**
Resource configuration of each node, such as 2-core 16 GB MEM.
- **Disk**
The main storage device of a computer, i.e., data storage space.
- **Balanced SSD**
It is based on Tencent Cloud's latest storage engine, NVMe SSD storage media and the latest network infrastructure. It employs a three-copy distributed mechanism to provide high-performance storage with low latency, high random IOPS, high throughput I/O, and data availability up to 99.9999999% (nine nines). It is applicable to business scenarios that have extremely high requirements for storage I/O performance and high-availability architecture at the application layer, such as online games, ecommerce, ERP software services, and video live streaming.
- **Enhanced SSD**
It is an entry-level all-flash block storage product provided by Tencent Cloud. It's highly cost-effective and suitable for medium applications with high requirements for data reliability and standard requirements for performance, such as web/app servers, business logical processing, KV services, as well as basic database services.
- **High-performance local SSD**
High-I/O local disk storage type.
- **SSD**
- It is an all-flash cloud disk storage type with NVMe SSD as the storage media. It adopts a three-copy distributed storage mechanism to provide low-latency and high-throughput I/O capabilities with a high random IOPS and 99.9999999% (nine nines) data security.
- **Premium cloud disk**
- It is a hybrid storage type. It provides high-performance storage capabilities close to SSD through the cache mechanism and adopts a three-copy distributed mechanism to ensure the data reliability.
- **Project**
Used to categorize and manage instance resources.
- **Tag**
A cloud resource management tool that allows you to use different standards to categorize, search for, and aggregate cloud resources with the same attributes.
- **Maintenance time**
To ensure the stability of your TencentDB instance, the backend system performs maintenance operations on the instance during the maintenance window from time to time. We highly recommend that you set an acceptable maintenance time for your business instance, usually during off-peak hours, so as to minimize the potential impact on your business.
- **Security group**
Security access control to instances by specifying IP, protocol, and port rules for instance access.
- **Network**
A network made up of several nodes and linkages that connect them. It represents many objects and their interconnections. For performance and security considerations, only VPC network is supported currently.
- **Private network address**
The IP and port assigned to a database for both read and write requests within your VPC network.
- **Port**
A port in a computer, switch, or router.
- **Database**
A set of organized, shared, and centrally managed data that is stored on a computer for a long period.
- **Database account**
A username used to log in to and manage a database.
- **Character set**
A mapping relationship or encoding rule, including a coded character set and character encoding. The code points corresponding to a character set are mapped into binary sequences, so that they can be stored and processed by a computer.
- **Cloud Virtual Machine (CVM)**
A scalable computing service provided by Tencent Cloud.
- **SSMS**
SQL Server Management Studio (SSMS) is an integrated environment to manage any SQL basic structures.
- **Alarm policy**
You can create alarms to stay informed of the status changes of certain metrics. The specific metrics will be monitored for a certain period of time, and alarm notifications will be sent by SMS, email, and phone at specified intervals based on the given threshold.
- **Pub/Sub**
Business data replication and sync. You can create, change, and delete pub/sub servers in the TencentDB for SQL Server console.
- **Recycle bin**
A place where terminated instances are stored before elimination. Such instances can be restored.
- **Backup**
Data is stored separately or as a file copy to tackle possible unexpected situations such as file or data loss or corruption.
- **Automatic backup**
You can set the backup time and cycle for the system to automatically and regularly save data.
- **Non-archive backup**
Automatic backups include non-archive backups and archive backups with different backup retention policies. For non-archive backups, you can set the backup retention period and time by week, and you should back up your data at least twice a week.
- **Archive backup**
Automatic backups include non-archive backups and archive backups with different backup retention policies. Archive backup is a more flexible backup policy on the basis of non-archive automatic backup. It supports setting the number of retained backups by month, quarter, or year and does not need to retain additional new backups. However, its retention period is different from (longer than) that of non-archive backup.
- **Manual backup**
You can manually create backup files at any time.
- **Data backup**
You can back up one, multiple, or all databases in an instance.
- **Log backup**
The system automatically generates a log backup (log file) every 30 minutes and uploads it to the cloud for storage. You can download log files.
- **Backup policy**
You can select instance backup or multi-database backup. The former backs up all databases in an instance, while the latter backs up selected databases.
- **Backup task configuration**
It is used to set the global variables of manual and scheduled backups. You can set **Upload Backup File** (archive file or unarchived files) and select the primary or replica instance for backup.
- **Backup file format**
It is used to set whether to upload an archive file or upload unarchived files for the instance.

