## Engine

Rocks and WiredTiger engines are supported.

## Replica Set and Sharded Cluster

You can create a TencentDB for MongoDB instance with either replica sets or sharded clusters:

| Node Configuration | Description |
| :------: | :----------------------------------------------------: |
| Replica set | 1 master, 2 slaves. Includes 1 Primary node and 2 Secondary nodes |
| Sharded cluster | A single instance contains at least 2 shards, and each shard consists of at least 3 nodes. Expandable. |

## Connection Count Limits

| MEM Specification | Max Connections |
| :------: | :------------: |
|   2GB    |      1500      |
|   4GB    |      1500      |
|   6GB    |      1500      |
|   8GB    |      1500      |
|   12GB   |      1500      |
|   16GB   |      2500      |
|   24GB   |      3500      |
|   32GB   |      4500      |
|   48GB   |      6000      |
|   64GB   |      9000      |
|  128GB   |     15000      |
|  240GB   |     15000      |
|  512GB   |     15000      |

>!The upper limit of the number of connections is at instance-level, instead of node-level.

## Connection User Name
TencentDB for MongoDB comes with two default users: "rwuser" and "mongouser". The role for the built-in users is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/). In other words, you only can read and write databases, but other critical operations are not permitted.
Depending on the version of TencentDB for MongoDB, some instances only have "rwuser" (Tencent Cloud will upgrade these instances and will contact you before the upgrades.).
You can also use TencentDB for MongoDB Console for account and permission management to meet your business needs.

## Avoiding Filling Up Disk
Write operation will be denied when the instance disk is 100% occupied, so please adjust instance configuration in time according to your business needs. For more information, see [Adjusting Instance Specification](https://cloud.tencent.com/document/product/240/19911). You can also [Contact us](https://cloud.tencent.com/about/connect) for assistance.
