[//]: # (chinagitpath:XXXXX)

### Overview
With the explosive growth of game data, it has become increasingly difficult for traditional relational databases to meet needs such as high concurrent read and write functions, efficient storage of and access to massive data, high scalability and high availability. In contrast, NoSQL databases have developed rapidly owing to their advantages like simple expansion and fast read and write functions.
Tencent Cloud TcaplusDB is specially built for game data storage based on the design concept and technology of non-relational databases. It can balance performance and cost according to the characteristics of games. So far, it has provided stable data storage services for multiple online games with tens of millions of DAU, such as Arena of Valor, CrossFire and NARUTO. With Tencent Cloud's infrastructure service nodes distributed on five continents (Asia, Europe, North America, South America and Oceania), game developers can use TcaplusDB all over the world after the first access.

### Product Introduction
TcaplusDB is a NoSQL distributed data storage service designed for games and it supports Protobuf API access. By combining Cache with disks, Tcaplus can deliver high performance while saving costs to support all-server/all-region and multi-region/multi-server structures. In addition, it provides safe, reliable and complete solutions covering capacity expansion/reduction with non-stop service, backup for disaster recovery, and quick rollback in response to the explosive data growth and long-tail OPS of games. It is now widely used in hundreds of popular games such as Arena of Valor, CrossFire and NARUTO.

### Features
#### Cache combined with persistent storage
Description: Cache and disk storage are combined, and hot and cold data are automatically swapped in/out.
User value: There is no need to use two kinds of databases, and thus the application architecture is simplified.
#### All-server/all-region support
Description: Storage space is uncapped, with a single table limited to 50 TB. Capacity expansion/reduction with non-stop service, as well as all-server/all-region and multi-server/multi-region are supported.
User value: There is no need to be concerned about storage space expansion.
#### PB access support
Description: Flexible data access is enabled by use of Protobuf, and access to and extraction of specified fields are supported.
User value: Bandwidth is greatly saved and cost is reduced.
#### Quick rollback
Description: Cold backup is pulled quickly and then parallel decompressed. The rollback process is entirely automated, and rollback to a precise time point is supported. With 300 GB cold data backup on each node, all nodes can be recovered within 2 hours.
User value: Quick rollback can reduce failure losses.
#### Backup for disaster recovery
Description: Overload protection; master/slave hot backup; daily cold backup for disaster recovery with data retained for up to 30 days, and Binlog record for 15 days.
User value: Data security is ensured and operation failure is handled easily.


### Strengths

#### High performance
Features including LRU-based exchange of hot and cold data between memory and disks, data storage on SSD disk and multi-server distribution of data ensure a high performance of up to 100,000 QPS per server with a latency less than 10 milliseconds.

#### High availability
The master/slave hot backup mechanism ensures quick recovery in case of system failure.

#### Low cost
The key-table NoSQL storage service, which employs memory storage supplemented by disk storage, provides the ability of switching in-process data between memory and disks, and the ability of dynamically expanding capacity across multiple processes to ensure that active data are stored in memory and inactive data on disks. This service saves about 70% in costs compared to memory-only storage, and about 40% in comparison to Redis+MySQL.

#### Dynamic expansion
The storage space is uncapped, and the capacity can be dynamically expanded or reduced according to the actual needs of a game without affecting game operation. This feature makes it easier to address sudden changes in business scale.

#### Ease of use
Various APIs are provided. Common operations (such as creating tables, altering tables, deleting tables, and cleaning data etc.) can be performed in web browsers, and OPS operations such as capacity expansion, capacity reduction, and backup are automatically performed.

#### Designed for games
All-server/all-region and multi-server/multi-region are both supported, and complete solutions covering capacity expansion/reduction with non-stop service, backup for disaster recovery, and quick rollback in response to the explosive data growth and long-tail OPS of games are provided. These features ensure the security and reliability of the service, making it the most suitable data storage service for games.

#### Global service
Relying on Tencent Cloud's infrastructure deployed around the globe, the service is accessible in more than 20 countries and regions on five continents.

