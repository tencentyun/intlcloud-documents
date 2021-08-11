## Problem Description
In some cases, the CPU utilization of certain nodes in a cluster is much higher than that of other nodes, which can be clearly observed in node monitoring in the ES console.

## Causes
- The design of index shards is inappropriate.
- The sizes of segments are uneven.
- There are typical scenarios with requirements for storage of hot and warm data.

## Troubleshooting
### Inappropriate shard settings
1. Log in to the Kibana console and run the following command in Dev Tools to view the index shard information. If nodes with a high load have more index shards, the shards are unevenly assigned:
```
GET _cat/shards?v
```
2. Log in to the Kibana console and run the following command in Dev Tools to view the index information. Check whether the node shards are unevenly assigned based on the cluster configuration:
```
GET _cat/indices?v
```
3. Assign shards again and appropriately plan them to ensure that the total number of primary and replica shards is an integer multiple of the number of data nodes in the cluster.
>!Elasticsearch also searches `.del` files during search and filters documents marked with `.del`, which reduces the search efficiency and wastes the specification resources. We recommend you force a merge during off-peak hours. For more information, please see [Force merge API](https://www.elastic.co/guide/en/elasticsearch/reference/7.5/indices-forcemerge.html).

#### Suggestions for shard planning
The shard size and quantity are two important factors affecting the stability and performance of an Elasticsearch cluster. All indexes in the cluster require appropriate shard planning; otherwise, large shards in unspecific businesses may incur excessive Elasticsearch performance overheads. The following are some suggestions for shard planning:
- Keep the size of a single shard of an index between 20 and 50 GB.
2. Add a time suffix to the index, so you can implement scrolling by time for easier management.
3. While following the principle of single shard design, predict the final index size and estimate the number of index shards based on the number of cluster nodes so as to distribute the shards among the nodes as evenly as possible.

>!More primary shards are not necessarily better, as the more the primary shards, the higher the Elasticsearch performance overheads. We recommend you keep the total number of shards per node 30 times of the node memory. If there are too many shards, file handles are very likely to be used up, causing cluster failures.

### Uneven segment sizes
1. Add `"profile": true` in the query body to check whether the `test` index has a shard whose query time is longer than that of other shards.
2. Specify `preference=_primary` and `preference=_replica` in the query separately and add `"profile": true` in the body to view the time it takes the primary and replica shards to make the query respectively. Check whether the primary or replica shard uses more time.
3. Log in to the Kibana console, run the following command in Dev Tools to view the shards, analyze the problem based on the segment information, and check whether the uneven loads are related to the uneven segment sizes.
```
GET _cat/segments/index?v&amp;h=shard,segment,size,size.momery,ip
GET _cat/shards?v
```
4. Solve the problem in either of the following methods:
 - Force a merge during off-peak hours. For more information, please see [Force merge API](https://www.elastic.co/guide/en/elasticsearch/reference/7.5/indices-forcemerge.html). Delete `delete.doc` in the cache completely and merge small segments into big ones.
 - Restart the node where the primary shard resides to trigger promoting the replica shard to the primary shard and generate a new replica shard. Data in the new primary shard is replicated to the new replica shard to ensure that they have the same segments.

### Typical scenarios with requirements for storage of hot and warm data
If you add `routing` in a query or query hotspot data with a high query frequency, uneven data load will definitely occur.
