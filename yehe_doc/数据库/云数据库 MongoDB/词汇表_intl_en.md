

### Region

A region refers to a geographical location where data centers hosted by Tencent Cloud are distributed. Each region has multiple availability zones.
For example, the region of one hosted data center is Beijing, and the availability zone is Beijing Zone 1. The cloud service products in the same region can communicate with each other through a private network, but those in different regions cannot. Thus, it is recommended to choose the region that is closest to your customers to minimize the access latency and improve download speed.



### Availability zone

An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network resources within a region. AZs are designed to ensure business stability because failures within an AZ are isolated without affecting other AZs within the same region.



### Database storage

Database storage is used to persistently store underlying storage resources of database data and logs.

### Number of database connections

Number of database connections refers to the number of sessions of the client connected to the database instance.

### Database migration

As business changes, the database also needs to be migrated from one environment to another along with application businesses, such as from a local IDC to a cloud platform or from a cloud platform to another one.

### Database instance

A database instance is a standalone database environment running in the cloud as the basic data block in TencentDB, which can contain multiple databases created by database users and can be accessed using the same client tools and applications as those for a standalone database instance.

### Database engine

Database engine is the core service for storing, processing, and protecting data. It allows you to control access permissions and process transactions quickly to meet the requirements of most applications for processing massive amounts of data in corporate scenarios. Database engine is supported by each database instance.



### TencentDB for MongoDB

TencentDB for MongoDB is a high-performance distributed data storage service created by Tencent Cloud based on MongoDB, the open source non-relational database. It is fully compatible with MongoDB protocol, and applicable to non-relational database-oriented scenarios.