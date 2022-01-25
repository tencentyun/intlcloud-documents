
## Strengths of TencentDB for MongoDB
TencentDB for MongoDB provides the capabilities of NoSQL databases as a service, which has great strengths in terms of flexibility, ease of use, high availability, fully managed OPS, data security, and data reliability. 

#### High flexibility and ease of use
- TencentDB for MongoDB is fully compatible with the open-source MongoDB protocol, so you can directly use MongoDB clients to communicate with TencentDB for MongoDB instances and migrate existing MongoDB applications to the cloud with no need to make any code modifications.
- TencentDB for MongoDB supports multiple system architectures to meet the needs in different business scenarios, including single node, replica set, and sharded cluster. You can deploy the most appropriate architecture according to your actual use case and adjust the configuration specifications promptly to adapt to use case changes.
- You can directly purchase TencentDB for MongoDB cluster instances on the purchase page, select the desired system architecture, and access the instances through URI with no need to install them on your own.

#### High availability
- The service can be deployed in a distributed cluster across AZs in a region-specific manner. This guarantees high service availability, and even failovers will not affect your normal business operations.
- With high-performance storage servers, the cluster can be quickly and elastically scaled to maintain a high throughput and an unlimited storage capacity when massive amounts of data are retained.

#### Fully managed service
- TencentDB for MongoDB is completely imperceptible to businesses. You can configure alarm rules in CM, which provides more than 20 automated monitoring metrics. This helps you stay up to date with the running status of your instances and promptly prevent risks.
- TencentDB for MongoDB offers a complete set of open management APIs to implement diverse self-service resource management and OPS features.

#### High security and reliability
- TencentDB for MongoDB supports configuring security groups in VPCs to implement allowlist-enabled network access control, which ensures the security and reliability of network environments.
- TencentDB for MongoDB supports authorization for Tencent Cloud root accounts and sub-accounts as well as cross-account authorization, which implements fine-grained resource control and enables enterprise-grade security protection.
- TencentDB for MongoDB supports multi-node data backup. It provides at least three online replicas of data storage to ensure data security and uses the data backup mechanism to store backup data for days and restore data in case of disasters.

## Differences Between TencentDB for MongoDB and Self-Built MongoDB
TencentDB for MongoDB offers special optimizations to solve issues which often occur during the operations of traditional self-built MongoDB instances, such as performance bottlenecks, OPS difficulties, as well as data reliability and availability problems. This makes it easier to deploy, manage, and scale instances. In addition, you can apply for required resources based on your actual business conditions and pay only for what you use in a more cost-effective way.

| Item | TencentDB for MongoDB | Self-Built MongoDB |
| :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Cost | You don't have to invest in hardware and software. Multiple specification options (such as High I/O and High IO (10 Gigabit)) are available for your choice. You can apply for required resources based on your actual business conditions and pay only for what you use. | A single storage server is costly. If you want a high-availability primary/secondary instance (replica set), you will have to purchase three servers, which may cause resource redundancy and waste. In addition, you need to recruit professional database administrators, which also means high labor costs. |
| Service availability | Hot backup is supported based on two or more servers, with automatic disaster recovery, failover, and imperceptible migration features available. In addition, the same read preference from the secondary databases as the native MongoDB is offered to ensure high read concurrency capability. | You need to fix failures and build primary/secondary replica cluster architecture and RAID on your own. |
| Data reliability | A 99.9996% data reliability is delivered along with comprehensive automatic data backup and lossless restoration mechanism, real-time hot backup, and data rollback to any time point in the last five days. Note: if the data manipulated between two backups exceeds the oplog size, you cannot roll it back to a time point between the two backups. | You need to protect your data on your own, and the data reliability is subject to hardware failure rate and database management skills of technical personnel. |
| System security | DDoS protection and fixes of various database and host security vulnerabilities are provided automatically. | You need to fix vulnerabilities on your own. |
| Real-Time monitoring | Multidimensional monitoring and automatic failure alarming are available in an unattended manner. | You need to develop your own monitoring system, and OPS personnel are often required to fix failures overnight, which incurs high OPS costs. |
| Business scaling | Quick scaling is available for fast deployment and service launch. | You need to procure hardware, host data centers, redeploy applications, and complete other tedious work on your own, which makes business scaling much slower. |
| Resource utilization | Resources can be requested on demand, achieving 100% resource utilization. | Business peaks are prone to cause low average load and low resource utilization. |
| Performance bottleneck   | New PCI-E SSD storage media and new-gen storage engines are adopted, with customizable performance tuning features to help improve the performance of specific components. | The open-source MongoDB is not specifically optimized, and its use is limited in certain scenarios.   |

