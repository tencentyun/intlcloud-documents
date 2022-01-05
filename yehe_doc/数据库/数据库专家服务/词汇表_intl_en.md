
### **Backup storage**
Backup storage is used to persistently store the underlying storage resources of database data and log backups.
### **Read/Write separation**
Read/Write separation allows the primary instance to perform transaction operations such as insertion, update, and deletion (INSERT, UPDATE, and DELETE) and the secondary instance (read-only) to perform SELECT query operations.


### **High reliability**
High reliability is often used to describe a system that is specifically designed to reduce downtime so as to maintain the high availability of its services.
### **Relational database**
Relational database is a database that is connected and organized based on relational data structure. For a relational database model, the complex data structure is simplified into a binary relation (a two-dimensional table). In a relational database, almost all data operations are performed on one or more relational tables. You can manage the database by sorting, joining, connecting, or selecting those related tables.
Common relational databases include Oracle, MySQL, MariaDB, Microsoft SQL Server, Access, DB2, PostgreSQL, Informix, and Sybase.
### **SSD**
Solid State Drive (SSD) disk is a disk made of an array of solid-state electronic memory chips. It is comprised of a control unit and a memory unit (FLASH chip and DRAM chip). The specification, definition, feature, and usage of the SSD disk interface are exactly the same as those of HDD disk interface. The shape and size of SSD disk are also identical to those of HDD disk. SSD disk is widely used in many fields, including vehicle, industrial control, video monitoring, network monitoring, network terminal, electric power, healthcare, aviation, and navigation equipment.


### **Logical backup**
Logical backup is a process during which data is extracted from a database and stored in a binary file through the SQL language. Logical backup allows you to use software technology to export data from the database and write it to an output file. The format of this file is generally different from that of files in the original database. This file is only an image of the data content in the original database. Therefore, the logical backup file can only be used for logical restoration of the database (i.e., data import) instead of physical restoration according to the original storage characteristics of the database. Logical backup is generally used for incremental backup of data changed after last backup.
### **Cold backup**
Cold backup is a backup method used when the system is shut down or under maintenance, which means that the data backed up is exactly the same as the data in the system.


### **QPS**
Queries per second (QPS) is a metric for measuring the amount of traffic processed by a particular query server within the specified period of time. 
### **Hot backup**
Hot backup is a backup method used when the system is running normally. In this case, since the data in the system is updated in real time, a lag may occur between the backup data and the real data of the system.
### **Data replication**
Data is replicated from the primary to the secondary in one of the following methods: strong sync replication, semi-sync replication, or async replication.
### **Database storage**
Database storage is used to persistently store underlying storage resources of database data and logs.
### **Database administrator**
A database administrator (DBA) is a person responsible for managing the database by using specialized software to store and organize data. The responsibilities of this role may include capacity planning, installation, configuration, database design, migration, performance monitoring, security, troubleshooting, and backup and restoration.
### **Number of database connections**
It refers to the number of sessions of the client connected to the database instance.
### **Database migration**
As business changes, the database also needs to be migrated from one environment to another along with application businesses, such as from a local IDC to a cloud platform or from a cloud platform to another one.
### **Database instance**
A database instance is a standalone database environment running in the cloud as the basic data block in TencentDB, which can contain multiple databases created by database users and can be accessed by using the same client tools and applications as those for a standalone database instance.
### **Database engine**
Database engine is the core service for storing, processing, and protecting data. It allows you to control access permissions and process transactions quickly to meet the requirements of most applications for processing massive amounts of data in enterprise scenarios. Database engine is supported by each database instance.

### **Physical backup**
Physical backup is a backup process in which the operating system files that actually make up the database are copied from one place to another (usually from a disk to a tape). Physical backup is divided into cold backup and hot backup.
