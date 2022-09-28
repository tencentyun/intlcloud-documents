## Overview

If the configuration of your purchased TencentDB for MongoDB instance isn't suitable for (either below or above) your current business requirements, you can quickly adjust its specifications based on your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

## Adjusting the specification

- The memory and CPU cores of mongod and mongos nodes are in fixed combinations, and the disk capacity has a corresponding value range. For example, if the specification of a mongod node is 2-core 4 GB MEM, then the disk capacity can range from 100 to 500 GB.

- Mongod replica nodes: You can select three (one-primary-two-replica), five (one-primary-four-replica), or seven (one-primary-six-replica) nodes in total. Currently, you cannot customize the number of replicas.
- The numbers of mongos nodes supported by single-AZ deployed and multi-AZ deployed instances are different. A single-AZ deployed instance can contain 3–32 nodes, while a multi-AZ deployed instance can contain 6–32 nodes.

You can select a specification based on your business conditions as described in [Product Specifications](https://intl.cloud.tencent.com/document/product/240/31183) first. Then, select an adjustment type and make adjustments based on the following table.

| Specification Adjustment Type                                                 | Specification Description                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Adjust the mongod node specification](https://intl.cloud.tencent.com/document/product/240/49133) | You can adjust the memory, disk capacity, and oplog capacity of a mongod node.             |
| [Adjust the replica node quantity](https://intl.cloud.tencent.com/document/product/240/49132) | You can add or remove replica nodes in both replica set and sharded cluster. You can select three (one-primary-two-replica), five (one-primary-four-replica), or seven (one-primary-six-replica) nodes in total. Currently, you cannot customize the number of replicas. |
| [Adjust the shard quantity](https://intl.cloud.tencent.com/document/product/240/49129) | You can add or remove mongod shards in a sharded cluster.                   |
| [Adjust the mongos node specification](https://intl.cloud.tencent.com/document/product/240/49133) | You can adjust the CPU cores and memory of mongos nodes in a sharded cluster.                    |
| [Adjust the mongos node quantity](https://intl.cloud.tencent.com/document/product/240/49127) | You can add mongos nodes in a sharded cluster.                         |
| [Add read-only nodes](https://intl.cloud.tencent.com/document/product/240/49130) | You can add 0–5 read-only nodes.                      |

