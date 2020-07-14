

### Region

A region refers to a geographical location where data centers hosted by Tencent Cloud are distributed. Each region has multiple availability zones.
For example, the region of one hosted data center is Beijing, and the availability zone is Beijing Zone 1. The Tencent Cloud services in the same region can communicate with each other through a private network, but those in different regions cannot. Thus, it is recommended to choose the region that is closest to your customers to minimize the access latency and improve download speed.

### Read/Write separation

Read/Write separation allows the master instance to perform transaction operations such as insertion, update, and deletion (INSERT, UPDATE, and DELETE) and the slave instance (read-only) to perform SELECT query operations.



### Availability zone

An availability zone (AZ) is a physical IDC of Tencent Cloud with independent power supply and network resources within a region. AZs are designed to ensure business stability because failures within an AZ are isolated without affecting other AZs within the same region.



### QPS

QPS (Queries per Second) measures the requests processed concurrently per second. 1 QPS means that the API processed 1 request per second; 50 QPS means that the API processed 50 requests per second.



### Database engine

Database engine is the core service for storing, processing, and protecting data. It allows you to control access permissions and process transactions quickly to meet the requirements of most applications for processing massive amounts of data in corporate scenarios. Database engine is supported by each database instance.



### TencentDB for Redis

TencentDB for Redis is a database provided by Tencent Cloud based on the Redis protocol and Tencent's years of technology experience in distributed caching, which features high availability, reliability, and flexibility. Compatible with Redis 2.8, 4.0, and 5.0 protocols and available in both standard and cluster architectures, it supports up to 4 TB of storage capacity and tens of millions of concurrent requests, meeting the needs of different scenarios such as caching, storage, and computing.