
This document describes the terms involved in TencentDB for MongoDB documentation to help you better understand various features.

**Instance**
An instance is a database environment that runs independently in Tencent Cloud. It is the basic unit in which you purchase TencentDB for MongoDB and exists as a separate process. One database instance can contain multiple user-created databases. You can create, modify, and delete instances in the console. Instances are independent of each other with resources isolated, thus avoiding the preemption of CPU, memory, and I/O.

**Region**
A region is the geographical location of a server for a TencentDB for MongoDB instance you purchase. Each region is completely independent. When you purchase instance resources, you need to specify the region closest to you in order to minimize the access latency, and the region cannot be changed after the purchase is made. In addition, as TencentDB for MongoDB needs be used with CVM, you should ensure that they are in the same region.

**Availability Zone**
Availability zones (AZs) refer to Tencent Cloud's physical data centers that are in the same region and have independent power supply and network resources. AZs communicate with each other over the private network to deliver a lower access latency. This ensures that failures within one AZ can be isolated (except for large-scale disasters or major power failures) without affecting other zones, guaranteeing your business stability.

**Replica Set**
A replica set is a primary/secondary cluster supported by TencentDB for MongoDB, which features automatic failover and consists of a primary node and one or more secondary nodes. It implements data redundancy and backup to increase data availability and ensure storage security. For more information on the architecture, see [System Architecture](https://intl.cloud.tencent.com/document/product/240/44173).

**Sharded Cluster**
A sharded cluster is another type of cluster supported by TencentDB for MongoDB and is suitable for storing massive amounts of data. By sharding data across multiple servers, a database system can store and process an ever-growing volume of data. Each sharded cluster consists of multiple components such as mongos, config servers, and shards. Each shard contains a subset of sharded data and is deployed as a replica set. For more information on the architecture, see [System Architecture](https://intl.cloud.tencent.com/document/product/240/44173).

**mongod**
mongod is the primary daemon process for the MongoDB system. It handles data requests, manages data access, and performs background management operations.

**mongos**  
mongos, short for "MongoDB shard", is a routing service configured for MongoDB sharding. It processes query requests from the application layer and determines the location of data in a sharded cluster to perform these operations.

**Shard**
A shard is a sharding server in a sharded cluster. It is a replica set with three nodes. You can purchase multiple shards to improve the data read/write concurrency performance.

**Config Server**
A config server in a sharded cluster stores the configuration of the metadata for all databases, such as routing and sharding information. mongos will load the configuration information from the config server upon its first start and every restart, and changes to the config server will also be notified to all mongos instances to ensure the routing accuracy.

[**Tencent Cloud console**](https://console.cloud.tencent.com/cdb)
Tencent Cloud console consists of web-based UIs.

**Classic Network**
Classic network is a network space shared by multiple users and cannot be divided. Its IP addresses are unique and randomly assigned and cannot be modified.

[**VPC**](https://intl.cloud.tencent.com/document/product/215/535)
A VPC is a custom virtual network space that is logically isolated from other resources.

[**Security Group**](https://intl.cloud.tencent.com/document/product/239/31945)
A security group controls the access to TencentDB for MongoDB instances by specifying IP, protocol, and port rules, so as to implement allowlist-enabled network control.

**Connections**
Connections refers to the number of TCP connections between the client and the TencentDB for MongoDB instance, i.e., the number of client sessions connected to the database instance. If the client uses a connection pool, the connections are persistent; otherwise, the connections are non-persistent. This metric is related to the specification of the database instance; in other words, the memory specification of the instance restricts the maximum number of connections. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/240/31183).

**Tag**
A tag is used to categorize and aggregate resources. If you have multiple types of TencentDB for MongoDB resources under your account which are correlated in many ways, you can use tags to group and categorize resources that have the same purpose or are associated with each other. In this way, when performing daily OPS or locating problems, you can quickly search for resources and perform batch operations to more efficiently fix failures.

**Project**
Project is a feature developed to help you better manage Tencent Cloud products. This feature is implemented on a project by project basis, and each Tencent Cloud product can be assigned to a project for easier management.

[**CVM**](https://intl.cloud.tencent.com/document/product/213)
Cloud Virtual Machine (CVM) is a scalable computing service provided by Tencent Cloud. You can access your TencentDB for MongoDB instance only by connecting to the private IP automatically assigned to it through CVM.

[**CAM**](https://intl.cloud.tencent.com/document/product/598)
Cloud Access Management (CAM) is a permission and user management system designed for secure and precise service management and access.

[**DTS**](https://intl.cloud.tencent.com/document/product/571)
Data Transmission Service (DTS) is a data transfer service that integrates such features as data migration, sync, and subscription, helping you migrate your databases without interrupting your business.

**Slow Log**
A slow log is used to log the command requests that are executed for a longer time than expected. Checking the volume of data in the slow log helps you promptly optimize the system performance.

**Rollback**
A rollback is an operation that restores backup data to minimize the losses caused by database maloperations. TencentDB for MongoDB provides multiple data restoration schemes to meet different data restoration needs in different scenarios.

