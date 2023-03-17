This document describes the specifications of replica set and sharded cluster instances supported by TencentDB for MongoDB to help you choose a specification suitable for your business.

## Replica Set
### Replica quantity
- Primary and secondary nodes: A one-primary-two-secondary architecture with three storage nodes is adopted by default. You can select five (one-primary-four-secondary) or seven (one-primary-six-secondary) nodes. Currently, you cannot customize the number of replicas.
- Read-only nodes: You can configure 0–5 secondary nodes as read-only nodes.

### Mongod specification

| CPU per Node | Memory per Node (GB) | Disk Capacity per Node (GB)         | Maximum Connections to Three Nodes |
| ------------- | ---------------- | ----------------------------- | --------------- |
| 2 cores            | 4 GB              | Default: 250 GB; range: [100,500]   | 3000             |
| 4 cores            | 8 GB              | Default: 500 GB; range: [150,1000]   | 6000             |
| 6 cores            | 16 GB             | Default: 750 GB; range: [250,1500]   | 9000             |
| 12 cores           | 32 GB             | Default: 1500 GB; range: [500,6000] | 12000            |
| 24 cores           | 64 GB             | Default: 2500 GB; range: [800,5000] | 18000            |
| 24 cores           | 128 GB            | Default: 3000 GB; range: [1500,5000] | 21000            |
| 32 cores           | 240 GB            | Default: 4000 GB; range: [1500,6000] | 42000            |
| 48 cores           | 512 GB            | Default: 4000 GB; range: [1500,6000] | 60000            |

## Sharded Cluster
### Mongod specification

| CPU per Node | Memory per Shard (GB) | Disk Capacity per Shard (GB)         |
| ------------- | ---------------- | ----------------------------- |
| 2 cores            | 4 GB              | Default: 250 GB; range: [100,500]   |
| 4 cores           | 8 GB              | Default: 500 GB; range: [150,1000]   |
| 6 cores           | 16 GB             | Default: 750 GB; range: [250,1500]   |
| 12 cores           | 32 GB             | Default: 1500 GB; range: [500,6000] |
| 24 cores           | 64 GB             | Default: 2500 GB; range: [800,5000] |
| 24 cores          | 128 GB            | Default: 3000 GB; range: [1500,5000] |
| 32 cores          | 240 GB            | Default: 4000 GB; range: [1500,6000] |
| 48 cores          | 512 GB            | Default: 4000 GB; range: [1500,6000] |

### Mongod shard quantity
Value range of the number of shards: [2,20].

### Node quantity per mongod shard
- Primary and secondary nodes: A one-primary-two-secondary architecture with three storage nodes is adopted by default. You can select five (one-primary-four-secondary) or seven (one-primary-six-secondary) nodes. Currently, you cannot customize the number of replicas.
- Read-only nodes: You can configure 0–5 secondary nodes as read-only nodes.

### Mongos specification
- A single-AZ deployed instance can contain 3–32 nodes.
- A multi-AZ deployed instance can contain 6–32 instances.

| Mongos Specification   | Maximum Connections per Mongos Node |
| ------------ | ---------------------- |
| 1-core 2 GB MEM   | 1000                   |
| 2-core 4 GB MEM   | 2000                   |
| 4-core 8 GB MEM   | 4000                   |
| 8-core 16 GB MEM  | 8000                   |
| 16-core 32 GB MEM | 16000                  |

### configServer specification 
The default configServer specification is **1-core 2 GB** with **20 GB** storage and **three replicas**, which cannot be modified. 


## User Name for Instance Connection
- TencentDB for MongoDB comes with a default user: "mongouser". It supports the SCRAM-SHA-1 authentication mechanism, and its role is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). You can use it to read and write any database, but are not permitted to perform high-risk operations.

- TencentDB for MongoDB v3.2 supports another default user: "rwuser". It uses the MONGODB-CR authentication mechanism which, however, has been no longer supported by MongoDB. We recommend that you use the "mongouser" to connect to your instance.

- You can also manage your account and permissions as needed in the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).

## Avoiding Filling Up Disk
If the disk usage of an instance has reached 100%, you cannot write to it. You need to adjust the instance specification in time or [contact us](https://intl.cloud.tencent.com/contact-us) for assistance. For more information, see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/240/31192).

