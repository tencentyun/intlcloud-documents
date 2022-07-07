## Limits on Region and AZ

The global replication feature can replicate data in the same AZ or across AZs between any Tencent Cloud regions no matter where instances in the replication group are deployed. Currently, only the following regions and AZs support global replication, and AZs of instances in a global replication group cannot be adjusted.

| Region | AZ |
| -------- | ------------------ |
| Hong Kong (China) | Hong Kong Zones 2 and 3 |
| Chengdu     | Chengdu Zone 1           |
| Virginia | Virginia Zone 2 |
| Shanghai | Shanghai Zones 5 and 6 |
| Beijing | Beijing Zones 5 and 7 |
| Guangzhou | Guangzhou Zones 4, 5, and 6 |
| Tianjin     | Tianjin Zone 2 |
| Nanjing | Nanjing Zones 2 and 3 |
| Singapore | Singapore Zone 2 |
| Shenzhen | Shenzhen Zone 4 |

## Limits on Global Replication Group Instance Version and Architecture

- Global replication supports instances running on 4.0 Standard Architecture, 4.0 Cluster Architecture, 5.0 Standard Architecture, and 5.0 Cluster Architecture.
- The architectures of instances in a global replication group cannot be changed; for example, you cannot change an instance from Cluster Architecture to Standard Architecture.
- The version and architecture of instances to be added to a global replication group must be the same as those of the master instance specified during group creation.

## Limits on Global Replication Group Instance Specifications

- An instance running on cluster architecture can have up to 64 shards in a global replication group.
- When creating a global replication group, you must specify a master instance with at least two replicas for the group.
- Currently, you can add up to four instances in a global replication group in the following deployment schemes: one master and three read-only instances, four master instances, or two master and two read-only instances.
- The specifications of instances to be added to a global replication group must be the same as those of existing instances in the group, and their memory capacity must be greater than or equal to the used capacity of the master instance specified during group creation.
- When you change the specification, all instances in a global replication group must have the same specification; otherwise, performance or capacity problems may occur.

## Limits on Parameter Settings

The `maxmemory-policy` parameter of instances in a global replication group must be set to `noeviction`.

## Limits on Command Sync

- The **FLUSHDB** or **FLUSHALL** command will be synced to all instances in the global replication group. Therefore, run them with caution.
- The **Pub** and **Sub** command groups will not be synced. We recommend you use the `Stream` data structure to replicate notification messages across regions.
- When the **RESTORE** command is synced, if the target instance has the same key, it will not be executed.

## Limits on Sync Granularity

Currently, the sync granularity is instance, that is, all instance data will be synced. You cannot choose to sync partial instance data.

