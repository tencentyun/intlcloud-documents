>?The monthly subscription mode is currently in beta test. To use it, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
>
## Billing Modes
TencentDB for MongoDB supports monthly subscription and pay-as-you-go billing modes.
#### Monthly subscription
Monthly subscription is a prepaid billing mode. It is applicable to long-term businesses with stable peak traffic, and is cheaper than the pay-as-you-go mode. To purchase a monthly subscription MongoDB instance, you need to pay for one or multiple months or even years in advance as needed.
#### Pay-as-you-go
Pay-as-you-go is a postpaid billing mode. We recommend you choose the pay-as-you-go billing mode if your business may fluctuate greatly and unpredictably or your resource usage tends to be temporary or abrupt. When you purchase a TencentDB for MongoDB instance, the hardware fees of one hour will be frozen in your Tencent Cloud account and charged on the hour (Beijing time), with the billable usage duration accurate down to the second. In this mode, you only need to pay for the actual usage of TencentDB for MongoDB with no upfront payment required.
The tiered pricing model is based on usage duration.

- 0 days < duration ≤ 4 days: tier 1 pay-as-you-go price applies.
- 4 days < duration ≤ 15 days: tier 2 pay-as-you-go price applies.
- Duration > 15 days: tier 3 pay-as-you-go price applies.

## Compute
Computing resources include CPU resources and memory resources. Instance parameters such as the maximum QPS and number of access connections are subject to the selected computing resource specification. For the prices, please see [MongoDB Pricing](https://intl.cloud.tencent.com/document/product/240/8364).

Currently, the following specifications are available:

| Configuration Type     | CPU per Node | Memory per Node | Instance QPS | Maximum Number of Connections |
| ------------ | ---------- | ---------- | -------- | -------------- |
| High IO     | 1 core        | 2 GB        | 3,000     | 1,500           |
| High IO     | 2 cores        | 4 GB        | 5,000     | 2,000           |
| High IO     | 2 cores        | 6 GB        | 5,000     | 2,500           |
| High IO     | 4 cores        | 8 GB        | 9,000     | 3,500           |
| High IO     | 6 cores        | 16 GB       | 20,000    | 6,000           |
| High IO     | 10 cores       | 24 GB       | 25,000    | 8,000           |
| High IO     | 12 cores       | 32 GB       | 27,000    | 9,500           |
| High IO     | 24 cores       | 64 GB       | 33,000    | 16,000          |
| Ten-Gigabit High IO | 2 cores        | 4 GB        | 5,000     | 2,000           |
| Ten-Gigabit High IO | 4 cores        | 8 GB        | 9,000     | 3,500           |
| Ten-Gigabit High IO | 6 cores        | 16 GB       | 20,000    | 6,000           |
| Ten-Gigabit High IO | 12 cores       | 32 GB       | 27,000    | 9,500           |
| Ten-Gigabit High IO | 24 cores       | 64 GB       | 33,000    | 16,000          |
| Ten-Gigabit High IO | 24 cores       | 128 GB      | 36,000    | 18,000          |
| Ten-Gigabit High IO | 32 cores       | 240 GB      | 39,000    | 18,000          |
| Ten-Gigabit High IO | 48 cores       | 512 GB      | 42,000    | 18,000          |

>?
>- The above numbers of connections have taken effect since August 10, 2020.
>- For a replica set, the maximum number of connections for an instance is as indicated in the table above; for a sharded cluster, the maximum number of connections is the `number of shards * specification of single shard` or `18,000`, whichever is smaller.
For example, if a sharded cluster instance has 3 shards, each with 64 GB memory, then as 16,000 * 3 = 48,000 > 18,000, the maximum number of connections for this cluster will be 18,000.

## Storage
Tencent Cloud provides flexible, affordable and user-friendly data storage devices for TencentDB for MongoDB instances. For more information on prices, see [MongoDB Pricing](https://intl.cloud.tencent.com/document/product/240/8364).

