## Overview
Horizontal splitting (sharding) is actually how a distributed database works. Each node takes part in computing and storing data, but only for a part of data. Therefore, no matter how your business grows, you can simply keep adding devices to the distributed cluster to meet the growing computing and storage needs.

## Sharding
 Sharding is to spread the data of a table into multiple independent physical database servers according to a defined rule to form an "independent" database "shard". Multiple shards together form a logically complete database instance.

- In a conventional standalone database, reads and writes of a complete table are done on only one physical storage device.
![](https://main.qcloudimg.com/raw/de72666e1d6aca2a929b0047f941e8c2.png)
- In a distributed database, according to the shardkey set during table creation, the system will automatically distribute data to different physical shards, but the table is still logically complete.
![](https://main.qcloudimg.com/raw/de007b8014a27a44ae78a76846240507.png)
- In TDSQL, the shardkey is generally required to determine the sharding dimension, and then sharding is performed using a field modulo operation (hash) scheme. The field used for hash calculation is shardkey. The hash algorithm can virtually guarantee relatively even distribution of data in different physical devices.

### Data writes (shardkey included in SQL statement)
1. The business writes a row of data.
2. The gateway performs hash calculation of the shardkey.
3. Different hash value ranges correspond to different shards (decided by the pre-sharding algorithm of the scheduling system).
4. Data is stored in the actually corresponding shard according to the sharding algorithm.
![](https://main.qcloudimg.com/raw/f0685bccd02ed8ff472ed236443db970.jpg)

## Data Aggregation
**Data aggregation**: If the data of a query SQL statement involves multiple sharded tables, the statement will be routed to all these tables for execution. TDSQL will aggregate the data returned by each sharded table based on the original SQL semantics and return the final result.
>When executing a SELECT statement, you are recommended to include the shardkey field; otherwise, the gateway may aggregate the execution results after a full table scan which is slow and affects the performance significantly.

### Data reads (specific shardkey included):
1. When the business sends a SELECT request including the shardkey, the gateway will perform a hash calculation on the shardkey.
2. Different hash value ranges correspond to different shards.
3. Data is obtained from the corresponding shard according to the sharding algorithm.

### Data reads (specific shardkey not included)
1. A SELECT request without the shardkey sent by the business will be sent to all shards.
2. Shards send back data to the proxy after querying their own content.
3. The proxy aggregates the data according to SQL rules and then responds to the gateway.
![](https://main.qcloudimg.com/raw/69e20f1aa0eb2c86c121dd3de9b40a40.png)
