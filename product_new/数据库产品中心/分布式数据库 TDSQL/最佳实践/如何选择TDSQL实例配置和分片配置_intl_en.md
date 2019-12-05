## TDSQL Selection Overview

A TDSQL instance is composed of shards. The specification and number of shards determine the processing capability of the instance. In theory:

- TDSQL instance read and write concurrency performance = ∑ (performance of a shard with a certain specification * number of shards)
- TDSQL instance transaction performance = ∑ (transaction performance of a shard with a certain specification * 70% * number of shards)

Therefore, the higher the shard specification and quantity, the stronger the processing capability of the instance. The performance of a shard is mainly subject to CPU/memory and measured by QPS. General performance metrics are detailed in the shard performance description section.


## TDSQL Shard Specification Selection

Specification of a TDSQL shard is determined by three factors: performance, capacity, and other requirements.

**Performance**: By predicting the performance demand and possible growth for at least 6 months, you can define the total CPU/memory size required of your distributed instance.
**Capacity**: By predicting the disk capacity and possible growth for at least one year, you can define the total disk size required of your distributed instance.
**Other requirements**: You are recommended to store at least **50 million rows of data** in one shard and take into account business needs such as [broadcast and non-sharded tables](https://intl.cloud.tencent.com/document/product/1042/33358) and in-node joins.

> Note: You are recommended to ensure high specification for a single shard while keeping the shard quantity relatively small.

Based on the above, it is estimated that you may have the following business requirements. Recommended strategies are as follows:

- For functional testing with no special performance requirements: 2 shards with **2 GB of memory and 25 GB of disk capacity each**.
- In initial stage of business when the total size of data is small but grows fast: 2 shards with **16 GB of memory and 200 GB of disk capacity each**.
- In stable development stage when sharding is based on actual business conditions: 4 shards, and the specification for each one should be **current business peak * growth rate / 4**.


## TDSQL Shard Performance Test

The database benchmark performance test is to modify the descriptions of sysbench 0.5: otlp script in sysbench is modified, and read/write ratio is set to 1:1 and controlled by executing test command parameters `oltp_point_selects` and `oltp_index_updates`. All test cases in this document perform 4 SELECT operations and 1 UPDATE operation to keep the read/write ratio at 4:1.

|vCPU (Core)|Memory (GB)|Storage Capacity (GB)|Data Set (GB)|Number of Clients|Single-client Concurrence|QPS|TPS|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|2 GB|100 GB|46 GB|1|128|1880|351|
|2|4 GB|200 GB|76 GB|1|128|3983|797|
|2|8 GB|200 GB|142 GB|1|128|6151|1210|
|4|16 GB|400 GB|238 GB|1|128|10098|2119|
|4|32 GB|700 GB|238 GB|2|128|20125|3549|
|8|64 GB|1 TB|378 GB|2|128|37956|7002|
|12|96 GB|1.5 TB|378 GB|3|128|51026|10591|
|16|120 GB|2 TB|378 GB|3|128|81050|15013|
|24|240 GB|3 TB|567 GB|4|128|96891|17698|
|48|480 GB|6 TB|567 GB|6|128|140256|26599|


> TPS here is for single transaction other than distributed transaction.
> 
> As required by operational strategies, current TDSQL instances (or part of them) adopt the policy of overuse of idle resources, so CPU utilization may exceed 100% on your monitoring panel.
