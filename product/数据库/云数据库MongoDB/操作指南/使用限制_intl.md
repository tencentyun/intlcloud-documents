## Engine

Rocks and WiredTiger engines are supported.

## Replica Set and Sharding Cluster

There are two options when creating a TencentDB for MongoDB instance:

| Node Configuration | Description |
| :------: | :----------------------------------------------------: |
| Replica set | 1 master, 2 slaves. Includes 1 Primary node and 2 Secondary nodes |
| Sharding cluster | A single instance contains at least 2 shards, and each shard consists of at least 3 nodes. It is expandable. |

## Limit on Number of Connections

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

>!The upper limit on the number of connections is applicable to instances rather than nodes.

## Connection User Name
TencentDB for MongoDB comes with two default users: "rwuser" and "mongouser". The role for the built-in users is [readWriteAnyDatabase+dbAdmin](https://docs.mongodb.org/v3.0/reference/built-in-roles/), that is, you can read and write any database, but are not permitted to perform critical operations.
Depending on the version of TencentDB for MongoDB, some instances only have "rwuser" (Tencent Cloud will upgrade such instances and will contact you before doing so).
You can also use the Console of TencentDB for MongoDB for account and permission management to meet your business needs.

## Avoiding Filling Up Disk
Write operation will be denied when the instance disk is 100% occupied, so please adjust instance configuration in time according to your business needs. For more information, see [Adjusting Instance Specification](https://cloud.tencent.com/document/product/240/19911). [Contact us](https://cloud.tencent.com/about/connect) if you encounter such situation.

