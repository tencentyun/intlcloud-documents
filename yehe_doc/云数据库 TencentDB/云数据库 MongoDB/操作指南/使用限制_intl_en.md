## Engine
Currently, Rocks and WiredTiger engines are supported.

## Replica Set and Sharded Cluster
There are two options available when you create a TencentDB for MongoDB instance:

| Node Configuration | Description |
| ------ | ---------------------------------------------------- |
| Replica set | 1 primary node and 2 secondary nodes |
| Sharded cluster | A single instance has at least 2 shards, each of which has at least 3 nodes and is scalable (currently, the shard node specifications are scalable, but the numbers of shards and nodes are not) |

## Limits on Number of Connections
For a replica set, the maximum number of connections is subject to the memory size of a single node as shown below:

| Memory Specification | Maximum Number of Connections |
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

>?
>- The above numbers of connections have taken effect since August 10, 2020.
>- For a sharded cluster, the maximum number of connections is the `number of shards * specification of single shard` or `20,000`, whichever is smaller.
>For example, if a sharded cluster instance has 3 shards, each with 64 GB memory, then as 16000 * 3 = 48000 > 20000, the maximum number of connections for this cluster will be 20,000.

## Connection Username
TencentDB for MongoDB comes with a default user: "mongouser". It supports the SCRAM-SHA-1 authentication mechanism, and its role is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). You can use it to read and write any database, but you are not permitted to perform high-risk operations.

TencentDB for MongoDB v3.2 supports another default user: "rwuser". It uses the MONGODB-CR authentication mechanism which, however, is no longer supported by MongoDB. We recommend you use the "mongouser" to connect to your instance.

You can also manage your account and permissions as needed in the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb).


## Avoiding Filling up Disk
If the disk utilization of an instance has reached 100%, you cannot write to it. Please adjust the instance specification in time as needed. For more information, please see [Adjusting Instance Specification](https://intl.cloud.tencent.com/document/product/240/31192). If this happens, please contact us for assistance.
