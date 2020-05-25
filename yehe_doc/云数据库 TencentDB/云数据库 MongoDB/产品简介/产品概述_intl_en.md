## Overview
TencentDB for MongoDB is a high-performance distributed data storage service created by Tencent Cloud based on MongoDB, an open-source non-relational database. It is fully compatible with the MongoDB protocol and applicable to various non-relational database-oriented scenarios.

>MongoDB® is a registered trademark of MongoDB, Inc. TencentDB for MongoDB is not authorized by or affiliated with MongoDB, Inc. Tencent's use of MongoDB software is based on open-source licenses.

## Features
- TencentDB for MongoDB offers cloud storage services, which are the data storage services provided for internet applications by Tencent Cloud.
- It is fully compatible with the MongoDB protocol and suitable for scenarios with traditional table structure, cache, non-relational data, as well as parallel large-scale data set computation using MapReduce.
- It provides high-performance, reliable, easy-to-use, and convenient MongoDB cluster services. Each instance is a replica set with at least one master and one slave or a sharded cluster that contains multiple replica sets.
- It offers backup, capacity expansion, and other features to ensure data security and dynamic scalability as much as possible.

## Product Architecture
The system architecture of TencentDB for MongoDB replica set is as follows:
![](https://main.qcloudimg.com/raw/3c8da14ce8ae9c5b0f8fd22ee8ed26eb.png)
Replica set v4.0 is different from other versions in architecture. It has no proxy set component, so you can directly access each node:
![](https://main.qcloudimg.com/raw/6596bc932409096fba195d55a8eb6532.jpg)
A sharded cluster consists of components such as shards, proxy sets, and config servers. Each shard contains a subset of sharded data. Each shard in TencentDB for MongoDB is deployed as a replica set:
![](https://main.qcloudimg.com/raw/8d32229843170d3e536ee6aff757a536.png)

