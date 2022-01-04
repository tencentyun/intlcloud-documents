<div class="tab_list">
<ul>
    <li><a href="#A-E">A-E</a></li>
    <li><a href="#F-J">F-J</a></li>
    <li><a href="#K-O">K-O</a></li>
    <li><a href="#P-T">P-T</a></li>
    
</ul>
</div>

<span id="A-E"></span>
## A-E 

### Automatic Backup
This refers to a full backup of the database instance automatically created by the system. You can configure the start time period and retention period of automatic backups.

### Backup Retention Period
This refers to the retention period of automatic backups. Backups that exceed the retention period will be automatically deleted.

### Backup Storage
This is used to persistently store database data, logs, or other underlying storage resources of backups.

### Database Admin
A database admin (DBA) is a person responsible for managing the database using specialized software storage and data organization. The responsibilities of this role include but not limited to capacity planning, installation, configuration, database design, migration, performance monitoring, security, troubleshooting, and backup and restoration.

### Database Instance
A database instance is a standalone database environment running in the cloud, which can contain multiple databases created by database users and can be accessed using the same client tools and applications as those for a standalone database instance.

### Database Instance Lifecycle
The lifecycle of a database instance is from the time it is created to its final release, during which operations such as backup, restoration, specification change, capacity expansion, restart, and deletion can be performed on the database.

### Database Migration
As business changes, the database also needs to be migrated from one environment to another along with application businesses, such as from a local IDC to a cloud or from a cloud to another one.

### Data Replication
In the master/slave high availability architecture, after the data is submitted to the master instance, it is copied to the slave instance, and this process is called data replication, which can usually be divided into strong sync replication, semisync replication, and async replication.

### Databases User Account
A database user account is different from your Tencent Cloud account and used only within the specified TencentDB instance environment to control access to your database instance. A database master user account is a local database user account that can be used to connect to a database instance. After a database instance is created, you can connect to the database using the database user account. You can also create additional database user accounts to meet your actual account needs.

<span id="F-J"></span>
## F-J 

### Failover
When an exceptional interruption occurs in a database instance, the system will automatically switch to a slave instance so to restore database operations as quickly as possible without administrative intervention. The time it takes to complete a failover depends on the database activities and other conditions when the master database instance becomes unavailable, which generally ranges from seconds to minutes.

### High Availability
High Availability is the system ability to function properly without interruptions. It is the degree of system availability.

### Hot Backup
This is a backup method when the system is running normally. In this case, data in the system is updated in real time, and a lag may occur between the backup data and the real data of the system.

### Instance ID
Each database instance has a database instance ID. The ID provided can uniquely identify the database instance when you interact with the console and APIs. The database instance ID must be unique at the region level.

### Instance Specification
The computing power and memory capacity of a database instance are determined by the database instance specification. You can change the CPU and memory available to a database instance by modifying its specification.

### IOPS
The input/output operations per second (IOPS) metric is reported as an average IOPS over a specified time period. The total IOPS is the sum of read IOPS and write IOPS. A typical value of IOPS ranges from zero to tens of thousands.


<span id="K-O"></span>
## K-O 

### Manual Backup
This is a full backup of a database instance initiated by you, and the backup file will be retained until you delete it manually.

### Master Database Instance
This is the database instance that provides read and write services among nodes that provide database services.

### Network Traffic
This refers to the network transfer throughput, which is the rate of the inbound and outbound network traffic of the database instance per second (in MB).

### Number of Database Connections
This refers to the number of sessions of the client connected to the database instance.

### Performance Metrics
Metrics that reflect the performance of a database instance, including but not limited to CPU utilization, memory utilization, storage utilization, network traffic, number of database connections, transaction rate/database throughput, submission latency, storage latency, storage IOPS, storage throughput, and storage queue depth.



<span id="P-T"></span>
## P-T 

### Relational Database
This is a database that is connected and organized based on relational data structure. For a relational database model, the complex data structure is simplified into a binary relation (a two-dimensional table). In a relational database, almost all data operations are performed on one or more relational tables. You can manage the database by sorting, joining, connecting, or selecting those related tables. Common relational databases include Oracle, MySQL, MariaDB, Microsoft SQL Server, Access, DB2, PostgreSQL, Informix, and Sybase.



### Transaction Rate/Database Throughput
The number of transactions completed in a specified time period is usually expressed in TPM (transactions per minute) or TPS (transactions per second). Another common term for transaction rate is database throughput. A database has a high transaction rate; therefore, it has a very low or zero disk throughput.

### Throughput/Disk Throughput
This refers to the number of bytes passed in or out of the disk per second. This metric is reported as the average throughput over a specified time period. The read throughput and write throughput are reported once per minute in megabytes per second (MB/s). A typical value of throughput ranges from zero to the maximum bandwidth of the I/O channel.







