## Overview
This document describes the fees of adjusting the configurations of a pay-as-you-go TencentDB for MongoDB instance. 

- **Replica set**: Configuration adjustment refers to adjusting the mongod configurations, including the mongod node computing specification and memory, disk capacity, number of primary and secondary nodes. After the adjustment, fees will be charged by the new configurations.
- **Sharded cluster**: Configuration adjustment refers to adjusting the mongod and mongos configurations, including the mongod shard quantity, node quantity per shard, and memory and storage capacity per node, as well as mongos computing specification, memory, and node quantity.

## Billing
### Upgrading instance configurations
#### Pay-as-you-go
The instance will be billed based on the new specification on the next hour under tier 1, and fees will be settled on each clock-hour.

- 0 days < duration ≤ 4 days: Tier 1 pay-as-you-go price applies.
- 4 days < duration ≤ 15 days: Tier 2 pay-as-you-go price applies.
- Duration > 15 days: Tier 3 pay-as-you-go price applies.

For detailed pricing, see [MongoDB Pricing](https://intl.cloud.tencent.com/document/product/240/8364).

### Downgrading instance configurations
#### Pay-as-you-go
The instance will be billed based on the new specification on the next hour under tier 1, and fees will be settled on each clock-hour.  
- 0 days < duration ≤ 4 days: Tier 1 pay-as-you-go price applies.
- 4 days < duration ≤ 15 days: Tier 2 pay-as-you-go price applies.
- Duration > 15 days: Tier 3 pay-as-you-go price applies.

For detailed pricing, see [MongoDB Pricing](https://intl.cloud.tencent.com/document/product/240/8364).
