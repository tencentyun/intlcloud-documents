This document describes the specifications of replica set and sharded cluster instances supported by TencentDB for MongoDB to help you choose a specification suitable for your business.

## Replica Set
### Number of replicas
A one-primary-two-secondary architecture with three storage nodes is supported by default. Currently, the number of replicas cannot be customized.

### mongod specifications

| CPU per Node | Memory per Node (GB) | Disk Capacity per Node (GB)         | Maximum Connections |
| ------------- | ---------------- | ---------------------------- | ---------------- |
| 2 cores            | 4 GB              | Default: 250 GB; range: [10,1500]   | 3000             |
| 4 cores            | 8 GB              | Default: 500 GB; range: [20,3000]   | 6000             |
| 6 cores            | 16 GB             | Default: 750 GB; range: [50,6000]   | 9000             |
| 12 cores           | 32 GB             | Default: 1500 GB; range: [100,6000] | 12000            |
| 24 cores           | 64 GB             | Default: 2500 GB; range: [100,6000] | 15000            |
| 24 cores           | 128 GB            | Default: 3000 GB; range: [100,6000] | 18000            |
| 32 cores           | 240 GB            | Default: 4000 GB; range: [100,6000] | 18000            |
| 48 cores           | 512 GB            | Default: 4000 GB; range: [100,6000] | 18000            |


## Sharded Cluster
### Number of shards
Value range of the number of shards: [2,20].

### Number of nodes per shard
A one-primary-two-secondary architecture is used for each shard by default. Currently, the number of nodes cannot be customized. 

### mongos specifications
mongos computing specifications include **2-core 4 GB**, **4-core 8 GB**, **8-core 16 GB**, and **16-core 32 GB**, and there can be 3–32 mongos instances. The maximum number of connections to a mongos instance is subject to the instance specification.

| mongos Specification  | Maximum Connections per mongos |
| ----------- | ---------------------- |
| 2-core 4 GB   | 1000                   |
| 4-core 8 GB   | 2000                   |
| 8-core 16 GB  | 3000                   |
| 16-core 32 GB | 9000                   |

### configServer specification 
The default configServer specification is **1-core 2 GB** with **20 GB** storage and **three replicas**, which cannot be modified. 

### mongod specifications

| CPU per Node | Memory per Shard (GB) | Disk Capacity per Shard (GB)         |
| ------------- | ---------------- | ---------------------------- |
| 2 cores            | 4 GB              | Default: 250 GB; range: [10,1500]   |
| 4 cores           | 8 GB              | Default: 500 GB; range: [20,3000]   |
| 6 cores           | 16 GB             | Default: 750 GB; range: [50,6000]   |
| 12 cores           | 32 GB             | Default: 1500 GB; range: [100,6000] |
| 24 cores           | 64 GB             | Default: 2500 GB; range: [100,6000] |
| 24 cores          | 128 GB            | Default: 3000 GB; range: [100,6000] |
| 32 cores          | 240 GB            | Default: 4000 GB; range: [100,6000] |
| 48 cores          | 512 GB            | Default: 4000 GB; range: [100,6000] |

## User Name for Instance Connection
- TencentDB for MongoDB comes with a default user: "mongouser". It supports the SCRAM-SHA-1 authentication mechanism, and its role is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). You can use it to read and write any database, but are not permitted to perform high-risk operations.

- TencentDB for MongoDB v3.2 supports another default user: "rwuser". It uses the MONGODB-CR authentication mechanism which, however, has been no longer supported by MongoDB. We recommend using the "mongouser" to connect to your instance.

- You can also manage your account and permissions as needed in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).

## Avoiding Filling Up Disk
If the disk usage of an instance has reached 100%, you cannot write to it. You need to adjust the instance specification in time or [contact us](https://intl.cloud.tencent.com/contact-us) for assistance. For more information, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/240/31192).

