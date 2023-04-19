## Overview
Horizontal partitioning (sharding) is actually how TDSQL for MySQL works. Each node takes part in computing and storing data, but only for a part of data. Therefore, no matter how your business grows, you can simply keep adding devices to the distributed cluster to meet the growing computing and storage needs.

## Horizontal Sharding
 Sharding means spreading the data of a table into multiple independent physical database servers according to a defined rule to form an "independent" database "shard". Multiple shards together form a logically complete database instance.

- In a conventional standalone database, reads and writes of a complete table are done on only one physical storage device.
![](https://main.qcloudimg.com/raw/de72666e1d6aca2a929b0047f941e8c2.png)
- In a distributed database, based on the shardkey set during table creation, the system automatically distributes data to different physical shards, but the table is still logically complete.
![](https://main.qcloudimg.com/raw/de007b8014a27a44ae78a76846240507.png)
- In TDSQL for MySQL, a shardkey is usually required to determine the sharding dimension, and then sharding is performed by using a field modulo operation (HASH) scheme. The field used for HASH calculation is the shardkey. The HASH algorithm can virtually guarantee relatively even distribution of data in different physical devices.

### Data writes (shardkey included in SQL statement)
1. The business writes a row of data.
2. The gateway hashes the shardkey to get its hash value.
3. Different hash value ranges correspond to different shards (determined by the pre-sharding algorithm of the scheduling system).
4. Data is stored in the corresponding shard according to the sharding algorithm.
![](https://main.qcloudimg.com/raw/f0685bccd02ed8ff472ed236443db970.jpg)

## Data Aggregation
Data aggregation: If the data of a query SQL statement involves multiple sharded tables, the statement will be routed to all these tables for execution. TDSQL for MySQL will aggregate the data returned by each sharded table based on the original SQL semantics and return the final result.
>!When you execute a SELECT statement, we recommend that you include the `shardKey` field; otherwise, the gateway may aggregate the execution results after a full-table scan which is slow and affects the performance significantly.

### Data reads (specific shardkey included):
1. When the business sends a SELECT request which includes the shardkey, the gateway will perform a hash calculation on the shardkey.
2. Different hash value ranges correspond to different shards.
3. Data is obtained from the corresponding shard according to the sharding algorithm.

### Data reads (specific shardkey excluded)
1. If the business sends a SELECT request without the shardkey, the request will be sent to all shards.
2. The shards send back data to the proxy after querying their own content.
3. The proxy aggregates the data according to SQL rules and then responds to the gateway.
![](https://main.qcloudimg.com/raw/69e20f1aa0eb2c86c121dd3de9b40a40.png)
