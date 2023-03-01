This document describes the strengths of TDSQL-C for MySQL.

## Full compatibility
TDSQL-C for MySQL separates the computing and storage capabilities of open-source databases. The storage is built on Tencent Cloud's distributed cloud storage service and the computing layer is compatible with open-source MySQL 5.7 and 8.0, so you can smoothly migrate your business without any modifications.

## Ultra high performance
The ultra high performance of a single node can sustain millions of QPS, which meets the requirements of high-concurrency and high-performance scenarios, ensures the continuity of key businesses, and provides better read/write separation and read/write scalability.

## Massive storage capacity
TDSQL-C for MySQL supports storage capacity at the petabyte level. It eliminates the need for frequent and tedious database sharding and table splitting operations otherwise required in the face of massive amounts of data. It also supports data compression and has been deeply optimized for data search and write.

## Fast disaster recovery
Compute nodes are stateless and support failover and recovery within seconds. Even if the physical machine where a compute node resides is down, it can be recovered in less than one minute.

## High data reliability
Clusters support security group and VPC network isolation and automatically maintain multiple replicas of data and backups to ensure data security and provide a data reliability of up to 99.9999999% (nine nines).

## Elastic scalability
Compute nodes can be quickly upgraded/downgraded and scaled within seconds as needed, which minimizes the costs of computing resources when coupled with elastic storage.

## Fast read-only scaling
1–15 read-only compute nodes can be quickly added in a cluster within seconds, enabling fast response to business surges and fluctuations.

## Snapshot backup and restoration
The fast snapshot backup feature based on multiple replicas of data provides continuous backup protection for your data and eliminates the need for the sync and migration of backup data in the source-replica architecture. Up to gigabytes of data can be rolled back per second, ensuring the rapid restoration of business data.

## Serverless architecture
TDSQL-C for MySQL Serverless Edition uses a serverless architecture to provide cloud native database services. It scales automatically and is pay-as-you-go, so you only pay for what you use. This helps you easily cope with dynamic changes and continuous growth of your business data volume.
