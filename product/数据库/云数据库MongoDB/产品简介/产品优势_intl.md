## Benefits of TencentDB for MongoDB
- **Convenient**: Users can quickly apply for cluster instance resources from the Tencent Cloud platform and directly access MongoDB instances through URI, without the need to install instances on their parts.
2. **Easy to use**: It is fully compatible with MongoDB protocol, and users can access instances via MongoDB protocol-based client. It can be used to seamlessly migrate existing MongoDB applications to the cloud platform.
3. **Secure**: At least three copies of online data storage are provided to ensure the security of online data. Meanwhile, the data backup mechanism stores backup data for several days to allow data recovery in case of disaster.
4. **High performance**: Centralized installation of dedicated high-performance storage server (all SSD models with high memory) to support massive access.
5. **Care-free**: 24/7 professional service is provided. Capacity expansion and migration operations are preceptionless to users and will not affect their services. Comprehensive monitoring features allow users to check the service quality of MongoDB at any time.

## Difference Between the TencentDB for MongoDB and Client's MongoDB
TencentDB for MongoDB provides the capabilities of NoSQL Database as a service, making itself easier to be deployed, managed, and expanded than client's MongoDB databases. At the same time, it has the same feature with the public cloud in terms of "Request on Demand and Pay by Usage" which improves its cost efficiency. See the following table for details:

| Item | TencentDB for MongoDB | Client's MongoDB |
| :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Cost | No need to invest in hardware and software and multiple options are available (high IO/high IO (10 GB)); pay on demand. | Hardware: a single storage server is costly. If a highly available master-slave instance (replica set) is required, you need to buy 3 units, causing resource redundancy.<br>Software: you need to recruit professional DBA personnel which means high labor costs. |
| Service availability | 99.95%, high industry standard, professional team on a 24/7 basis, one-to-one instruction, and QQ remote assistance. | Deal with failures and build master/slave or RAID by yourself. |
| Data reliability | 99.9996%, perfect auto data backup and lossless recovery mechanism, real-time hot backup, and recover data to any time point within 5 days. Note: If the data operated between the two backups exceeds the oplog size, you cannot roll it back to the time between the two backups. | Self-protection, and reliability depends on hardware failure rate and on the database management skills of technical personnel. |
| System security | Anti-DDoS attacks; repair various database and host security vulnerabilities in time. | Self-deployed with high costs; you need to repair database security vulnerabilities on your own. |
| Real-time monitoring | Multi-dimensional monitoring, and failure warning for ease of use. | You need to develop your own monitoring system, and OPS personnel are required to repair failures overnight. |
| Business scaling-up | One-click scaling-up on demand, fast deployment, and early on-line for ease of use. | You need to procure hardware, host data centers, redeploy applications and complete other work on your own with a longer cycle. |
| Resource utilization | Request on demand and 100% resource utilization to save your budget. | Peak period will cause low average load and low resource utilization rate. |

TencentDB for MongoDB has implanted special optimizations to resolve issues which often occur during the operations of traditional client's MongoDB, including performance bottleneck, OPS difficulties, data reliability, and availability problems:
- **Boost performance**: It adopts brand-new PCI-E SSD storage media and new generation storage engine, and provides customizable performance enhancing features to help users enhance the performance of specified components.
2 **Reduce OPS difficulty**: It features automatic monitor alarm for over 20 monitoring metrics, and supports bulk data import/export and templated parameter modification to make it easy for business deployment.
3 **Ensure highly available service**: It supports master-slave or even more hot backups, automatic disaster recovery, and failover is perceptionless to users. It also offers the same "read slave first" feature as the native MongoDB to ensure high concurrent read capability.
4 **Guarantee Highly reliable data**: It allows free data backup within 7 days, and supports private network firewall and public network DDoS protection.



