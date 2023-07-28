## Supported Versions
Currently, TencentDB for MySQL supports MySQL 5.5, 5.6, 5.7, and 8.0. For more information on the features of each version, see the [official documentation](https://dev.mysql.com/doc/refman/5.7/en/). MySQL's official lifecycle support policies are as shown below:

| Release            | GA Date | Premier Support End | Extended Support End | Sustaining Support End |
| :------------------ | :------- | :------------ | :------------- | :-----------|
| MySQL Database 5.0 | Oct-05  | Dec-11              | Not Available        | Indefinite             |
| MySQL Database 5.1 | Dec-08  | Dec-13              | Not Available        | Indefinite             |
| MySQL Database 5.5 | Dec-10  | Dec-15              | Dec-18               | Indefinite             |
| MySQL Database 5.6 | Feb-13  | Feb-18              | Feb-21               | Indefinite             |
| MySQL Database 5.7 | Oct-15  | Oct-20              | Oct-23               | Indefinite             |
| MySQL Database 8.0 | Apr-18  | Apr-23              | Apr-26               | Indefinite             |

>?
> - The extended official support for MySQL 5.5 ended in December 2018. There has been no explicit statement on further support extension, which is possibly because fixing issues takes more time. We strongly recommend that you use a higher version of MySQL.
> - MySQL 5.6 and higher no longer support the MyISAM storage engine, so we recommend that you use the InnoDB engine, which features better and more stable performance.
> - Currently, MySQL 5.6 and higher support three replication modes: async, semi-sync, and strong sync. Only async mode is available in MySQL 5.5.


## TencentDB for MySQL 8.0 Strengths
- Combined with a complete set of management services and the TXSQL kernel, TencentDB for MySQL provides an enterprise-level database service that is more stable and quicker to deploy. It applies to various use cases and helps you upgrade your business.
- TXSQL is 100% compatible with MySQL and the widely-used MySQL forks.
- TencentDB for MySQL supports three disaster recovery systems including hot standby, cold standby, and multi-AZ switchover. It can achieve up to 99.95% service availability and up to 99.9996% data reliability.
- TencentDB for MySQL offers a series of easy-to-use database management services, including monitoring, backup, rollback, encryption, auto scaling, auditing, and intelligent diagnosis and optimization. With these services, you can focus more on your business development.
- A TencentDB for MySQL instance can handle 500,000+ QPS. TencentDB for MySQL greatly simplifies business development, database Ops, and business architecture, making it easy for you to manage databases.
- It offers three architecture options: single-node, two-node, and three-node.
- It supports CStore, a high-performance columnar storage engine that allows for millions of real-time writes per second and millisecond-level queries on tens of billions of data points in any dimension. To apply for CStore, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Feature Comparison between TencentDB for MySQL 8.0 and Oracle MySQL 8.0

| Feature | TencentDB for MySQL 8.0                                 | Oracle MySQL 8.0                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Cost performance | 1. Elastic resources. <br>2. Tencent's kernel TXSQL. <br>3. Integrated backup and restoration features. <br>4. A complete set of SaaS tools and services. | 1. Huge one-time investment cost. <br>2. The open source version has no performance optimization. <br>3. Additional backup resources and costs. <br>4. Public network fees and high domain name fees. |
| Availability | 1. A complete high-availability switchover system is provided. <br>2. Read-only instances automatically balance load and traffic. <br>3. Disaster recovery instances are provided for remote disaster recovery, ensuring high availability. | 1. You need to buy servers and wait for the delivery. <br>2. You need to deploy the high availability and load balancing systems by yourself. <br>3. It costs a lot to build data centers in multiple regions. |
| Reliability | 1. Data reliability of up to 99.9996%. <br>2. Low RPO/RTO. <br>3. Stable source-replica data replication. | 1. Data reliability of 99%, which depends on the probability of damage to a single disk. <br>2. You need extra R&D investment to achieve a low RPO. <br>3. Data replication delays or interruptions may occur. |
| Ease of use | 1. A complete set of database management services are provided and databases can be easily operated in the console. <br>2. Second-level monitoring and intelligent alarms. <br>3. Automatic multi-AZ high-availability capability. <br>4. One-click version upgrade. | 1. You need to deploy high availability and backup and restoration systems by yourself, which requires time and money. <br>2. You need extra investment to purchase a monitoring system. <br>3. It costs a lot to set up data centers in different regions with labor costs in Ops. <br>4. The version upgrade cost is high and the maintenance needs a long downtime. |
| Performance   | 1. Local SSD disks have excellent performance and the custom hardware supports fast iterations. <br>2. The optimized TXSQL ensures high performance. <br>3. DBbrain supports the intelligent diagnosis and optimization of MySQL. | 1. Oracle MySQL has a slower hardware iteration speed than that of cloud computing, usually resulting in lower performance. <br>2. It can be costly as database maintenance relies on senior DBAs. <br>3. Oracle MySQL does not have native performance tools, so you have to purchase or deploy them by yourself. |
| Security   | 1. Prevention in advance: allowlist, security group, VPC-based isolation. <br>2. Protection during the database operations: TDE + KMS data encryption. <br>3. Auditing after the database operations: SQL auditing. <br>4. TencentDB for MySQL is updated right after the Oracle MySQL has security updates. | 1. The cost of the allowlist configuration is high and the private network needs to be implemented by yourself. <br>2. You need to implement encryption by yourself during the database operations. <br>3. It is difficult to audit SQLs after the database operations as the open-source MySQL does not support SQL auditing. <br>4. Once MySQL updates, Ops will be required to install updates or databases will have to be shut down for maintenance. |

## Performance Comparison between TencentDB for MySQL 8.0 and Oracle MySQL 8.0
#### Read performance
![](https://main.qcloudimg.com/raw/1bf9f7294ca6b4631f203333819ab2a1.png)

#### Write performance
![](https://main.qcloudimg.com/raw/f77b34eb5c769539325b2f04a539ad4f.png)

