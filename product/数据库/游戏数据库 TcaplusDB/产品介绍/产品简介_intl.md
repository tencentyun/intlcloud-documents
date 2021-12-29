## Overview
With the explosive growth of game data, it has become increasingly difficult for traditional relational databases to meet needs such as high concurrent read and write functions, efficient storage of and access to massive data, high scalability and high availability. In contrast, NoSQL databases have developed rapidly owing to their advantages like simple expansion and fast read and write functions.
TencentDB for TcaplusDB is specially built for game data storage based on the design concept and technology of non-relational databases. It can balance performance and cost according to the characteristics of games. So far, it has provided stable data storage services for multiple online games with tens of millions of DAU, such as Arena of Valor, CrossFire and NARUTO.

## Introduction
TencentDB for TcaplusDB is a NoSQL distributed data storage service designed for games and it supports [Protobuf](https://intl.cloud.tencent.com/document/product/1016/30295#P) API access. By combining cache with disks, TcaplusDB can deliver high performance while saving costs to support all-server/all-region and multi-server/multi-region structures. In addition, it provides safe, reliable and complete solutions covering capacity expansion/reduction with non-stop service, backup for disaster recovery, and quick rollback in response to the explosive data growth and long-tail OPS of games. It is now widely used in hundreds of popular games such as Arena of Valor, CrossFire and NARUTO.

## Features
#### Cache combined with persistent storage
Description: Cache and disk storage are combined, and hot and cold data are automatically swapped in/out.
User value: There is no need to use two kinds of databases, and thus the application architecture is simplified.
#### All-server/all-region support
Description: Storage space is uncapped, with a single table limited to 50 TB. Capacity expansion/reduction with non-stop service, as well as all-server/all-region and multi-server/multi-region are supported.
User value: There is no need concern about storage space expansion.
#### PB access support
Description: Flexible data access is enabled by use of Protobuf, and access to and extraction of specified fields are supported.
User value: Bandwidth is greatly saved and cost is reduced.
#### Quick rollback
Description: Cold backup is pulled quickly and then parallel decompressed. The rollback process is entirely automated, and rollback to a precise time point is supported. With 300 GB cold data backup on each node, all nodes can be recovered within 2 hours.
User value: Quick rollback can reduce failure losses.
#### Backup for disaster recovery
Description: overload protection; primary/secondary hot backup; daily cold backup for disaster recovery with data retained for up to 7 days and binlog records for 7 days.
User value: Data security is ensured and operation failure is handled easily.
