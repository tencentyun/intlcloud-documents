
This document describes the cost of adjusting the configurations of a pay-as-you-go TencentDB for MongoDB instance. 

## Background
Instance price will be recalculated after the instance configurations are adjusted, such as node memory, storage capacity, the number of nodes in a replica set, the number of shards in a sharded cluster, the number of nodes in a shard, etc.

## Billing
### Upgrading instance configurations
- Pay-as-You-Go instances are billed for every clock-hour (Beijing time). After the configuration adjustment is completed, fees for the next clock-hour will be calculated based on the price of the new configuration.

### Downgrading instance configurations
#### Pay-as-You-Go
Pay-as-You-Go instances are billed for every clock-hour (Beijing time). After the configuration adjustment is completed, fees for the next clock-hour will be calculated based on the tier 1 price of the new configuration.  
- 0 days < duration ≤ 4 days: tier 1 pay-as-you-go price applies.
- 4 days < duration ≤ 15 days: tier 2 pay-as-you-go price applies.
- Duration > 15 days: tier 3 pay-as-you-go price applies.

For detailed pricing, see [MongoDB Pricing](https://intl.cloud.tencent.com/document/product/240/8364).
