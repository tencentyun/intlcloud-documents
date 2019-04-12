## TencentDB for MongoDB Advantages
1. **Convenient**: It enables users to quickly set up MongoDB instances in Tencent Cloud environment, where you can directly access MongoDB instances through URI with no installments needed. <br/>
2. **Easy to use**: It is fully compatible with MongoDB protocol, so you can access instances via MongoDB protocol-based client and seamlessly migrate your existing MongoDB applications to the cloud platform. <br/>
3. **Secure**: It provides online backup (at least three copies) of your data to ensure data security. The data backup system also allows you to restore your data to several days ago for disaster recovery. <br/>
4. **High performance**:  It deploys high-performance, high density, high capacity SSD storage servers for handling high-frequency access requests. <br/>
5. **Care-free**: It provides 24/7 professional, downtime-free, transparent service of server capacity expansion and data migration; enables comprehensive monitoring features for real-time service quality assessment. <br/>

## TencentDB for MongoDB vs. Self-hosted MongoDB
TencentDB for MongoDB provides NoSQL service and is much easier to deploy, manage, and expand compared to on-premises MongoDB database. Like other cloud products, it supports order-on-demand and pay-as-you-use to improve your cost efficiency. See the following table for details:

| Item | TencentDB for MongoDB | Self-hosted MongoDB |
| :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Cost | Zero expense on hardware and software with multiple server options available (high IO/high IO (10 GB)); pay-as-you-use | Hardware: high hardware cost - a single storage server is expensive (you need to buy 3 machines to build a highly available master-slave replication set, causing resource redundancy).Software: high labor cost - Professional database administrators are needed.|
| Service availability | 99.95%, high industry standard, 24/7 professional service, one-on-one instruction, QQ remote assistance | Need to solve failures and build master/slave or RAID by yourself. |
| Reliability | 99.9996%, almost perfect auto data backup and lossless recovery mechanism, real-time hot backup that allows you to restore your data anytime within the last 5 days. Note: If the size of the data operated between two backups exceeds the oplog size, you cannot roll it back to a time between the two backups. | The reliability depends on the hardware failure rate and on the database management skills of technical personnel. |
| System security | Anti-DDoS attacks; repair various database and host security vulnerabilities in time. |  High costs; you need to fix database security vulnerabilities on your own. |
| Real-time monitoring | Multi-dimensional monitoring, and failure warning for ease of use. | You need to develop your own monitoring system, and OPS personnel are required to repair failures overnight. |
| Business scale-out | You can scale on-demand capacity through just one click with fast deployment. | You need to spend extra time on purchasing hardware, hosting data centers, and redeploying applications. |
| Resource utilization | Request on demand and 100% resource utilization to reduce your cost. | You have to spend on extra resources during peak periods, which lowers the average load and thus resource utilization rate. |

TencentDB for MongoDB can resolve common self-hosted MongoDB operation issues, such as performance bottlenecks, OPS difficulties, data reliability, and availability problems:
1. **Break performance bottleneck**: It adopts brand-new PCI-E SSD storage media and new generation storage engine; it provides customizable performance enhancing features to help improve your database performance. <br/>
2. **Reduce OPS difficulty**: It features automatic monitor alarm for over 20 monitoring metrics and supports Big Data import/export and templated parameter modification to make it easy for business deployment. <br/>
3. **High service availability**: It supports MongoDB master-slave with added hot backups for automatic disaster recovery and failover and the process is transparent to users. Like MongoDB, it allows you to read data from the slave first native MongoDB, which ensures high concurrent-read capability. <br/>
4. **High reliability**: It supports free data backup within 7 days, and enables private network firewall and public network DDoS protection. <br/>
