## Engine
Rocks and WiredTiger engines are supported.

## Replica Set and Sharded Cluster
There are two options when you create a TencentDB for MongoDB instance:

| Node Configuration | Description |
| ------ | ---------------------------------------------------- |
| Replica set | An instance has 1 primary node and 2 secondary nodes.|
| Sharded cluster |    An instance has at least 2 shards, and each shard has at least 3 nodes. You can expand the specifications of shard nodes, but cannot add shards or nodes.   |

## Limit on Number of Connections
| MEM Specification | Max Connections |
| :------: | :--------: |
|   2 GB    |    1,500    |
|   4 GB    |    2,000    |
|   6 GB    |    2,500    |
|   8 GB    |    3,500    |
|   16 GB   |    6,000    |
|   24 GB   |    8,000    |
|   32 GB   |    9,500    |
|   64 GB   |   16,000    |
|  128 GB   |   18,000    |
|  240 GB   |   18,000    |
|  512 GB   |   20,000    |

>!For a replica set instance, the maximum number of connections applies to the whole instance instead of a node; for a sharded cluster instance, it applies to a shard.

## User Name for Instance Connection
TencentDB for MongoDB comes with a default user: "mongouser". It supports the SCRAM-SHA-1 authentication mechanism, and its role is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). You can use it to read and write any database, but are not permitted to perform high-risk operations.

TencentDB for MongoDB v3.2 supports another default user: "rwuser". It uses the MONGODB-CR authentication mechanism which, however, has been no longer supported by MongoDB. We recommend using the "mongouser" to connect to your instance.

You can also manage your account and permissions as needed in the [MongoDB Console](https://console.cloud.tencent.com/mongodb).


## Avoiding Filling Up Disk
If the disk usage of an instance has reached 100%, you cannot write to it. Please adjust the instance specifications in time as needed. For more information, please see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/240/31192).
