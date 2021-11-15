## Benefits of TencentDB for MongoDB

- **Convenience**: you can quickly apply for cluster instance resources from the Tencent Cloud platform and directly access MongoDB instances through URIs without the need to install instances on your own.
- **Ease of use**: it is fully compatible with MongoDB protocols, so you can access instances by using MongoDB protocol-based clients. It can be used to seamlessly migrate existing MongoDB applications to the cloud.
- **Security**: at least three online replicas of data storage are provided to ensure data security. Meanwhile, the data backup mechanism stores backup data for days for data recovery in case of disaster.
- **High performance**: dedicated high-performance storage servers (with SSD disks and large memories) are installed in a centralized manner to support high numbers of access requests.
- **Carefree usage**: 24/7 professional customer service is provided. Capacity expansion and migration operations are imperceptible to your business and will not affect the service. Comprehensive monitoring features allow you to check the service quality of MongoDB at any time.

## Differences Between TencentDB for MongoDB and Self-built MongoDB
TencentDB for MongoDB provides the capabilities of NoSQL databases as a service, making itself easier to be deployed, managed, and expanded than your self-built MongoDB databases. In addition, it is pay-as-you-go and allows resource request on demand just like a public cloud, which further improves its cost efficiency. Please see the table below for details:

| Item | TencentDB for MongoDB | Self-built MongoDB |
| :--------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Cost | You don't have to invest in hardware and software. Multiple pay-as-you-go options (High IO/Ten-Gigabit High IO) are available for your choice. | Hardware: a single storage server is costly. If you want a high-availability master/slave instance (replica set), you will have to purchase three servers, causing resource redundancy. <br>Software: you need to recruit professional DBAs, which means high labor costs. |
| Service availability | An industry-leading availability of 99.95% is delivered. 24/7 professional customer service, as well as one-to-one instruction and QQ remote assistance, is provided. | You have to deal with failures and build primary/secondary instances or RAIDs on your own. |
| Data reliability | A 99.9996% data reliability, comprehensive automatic data backup and lossless restoration mechanism, real-time hot backup, and data rollback to any time point in the last five days are offered. Note: if the data manipulated between two backups exceeds the oplog size, you cannot roll it back to a time point between the two backups. | You have to protect your data on your own, and the data reliability is subject to hardware failure rate and database management skills of technical personnel. |
| System security | DDoS protection and fixes of various database and host security vulnerabilities are provided in time. | You have to deploy security services and fix vulnerabilities on your own. |
| Real-time monitoring | Unattended multidimensional monitoring and auto-alarming are available. | You have to develop your own monitoring system, and OPS personnel are often required to repair failures overnight. |
| Business scaling | Quick scale-out is available for fast deployment and service launch. | You have to procure hardware, host data centers, redeploy applications, and complete other tedious work on your own, which makes business scaling much slower. |
| Resource utilization | Resource requests can be made on demand to achieve 100% resource utilization. | Business peaks are prone to lead to low average load and low resource utilization. |

TencentDB for MongoDB offers special optimizations to solve issues which often occur during the operations of traditional self-built MongoDB instances, such as performance bottleneck, OPS difficulties, data reliability, and availability problems:
- **Boosted performance**: it adopts brand-new PCI-E SSD storage media and new-gen storage engines with customizable performance enhancing features to help improve the performance of specific components.
2. **Reduced OPS difficulty**: it features automatic monitoring and alarming for over 20 metrics and supports batch data import/export and templated parameter modification, making business deployment simpler.
3. **High service availability**: it supports hot backup based on two or more servers, automatic disaster recovery, and imperceptible failover. In addition, it offers the same read preference from the slave as the native MongoDB to ensure high concurrent read capability.
4. **High data reliability**: it enables backup of data within 7 days free of charge and supports private network firewall and public network DDoS protection.


