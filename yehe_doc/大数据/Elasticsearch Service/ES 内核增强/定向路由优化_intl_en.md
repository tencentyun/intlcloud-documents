## Background
In a larger cluster (with 100+ nodes), a single index generally has many shards (100+).

Users generally write in bulk, and ES uses `\_id` as the routing for writing a single document by default, so that shards can be distributed through routing. Such a bulk request will be evenly split into write subrequests of the number of shards, which will be then sent to each shard for writing. The coordinator node needs to wait for all shards to be written before returning to the client. If the number of shards is too large, long-tail subrequests appear easily, that is, some subrequests may be delayed in responding due to node failures, Old GC, network jitters, etc., resulting in the slow response and heap of the entire bulk request and eventually causing the node write queue to fill up. At this time, write rejection will occur. Moreover, splitting one bulk request into too many subrequests cannot increase the write throughput of data nodes and cannot make full use of the CPU.

## Optimized Scheme
In the multi-shard bulk write scenario, one bulk request is written to only one shard through routing, which reduces the network overheads, increases the CPU utilization of data nodes, and prevents long-tail shards from affecting the entire bulk request.

The ES kernel provides an index attribute that can uniformly and automatically add a random routing for each write subrequest of a bulk request, ensuring that one subrequest is only routed to one shard and that the data of each shard is balanced in the index.

## Directions
The new index attribute is **index.bulk_routing.enabled**, and its default value is `false`, which can be specified during index creation or dynamically updated subsequently.

Specify to enable bulk routing optimization when creating an index:
```
curl -X PUT "localhost:9200/my-index" -H 'Content-Type: application/json' -d'
{
    "settings" : {
        "index" : {
            "bulk_routing.enabled" : true
        }
    }
}
'
```
Dynamically update a single index:
```
curl -X PUT "localhost:9200/my-index/_settings?pretty" -H 'Content-Type: application/json' -d'
{
  "index.bulk_routing.enabled": true
}
'
```
Generally, a template can be created for multiple indexes of the same business type, which can take effect in batches in index rolling scenarios:
```
curl -X PUT "localhost:9200/_template/bulk_routing_template?pretty" -H 'Content-Type: application/json' -d'
{
  "index_patterns": ["indices-prefix*"],
  "settings": {
    "bulk_routing.enabled": true
  }
}
'
```

## Optimization Limits
### Write limits
After bulk routing optimization is enabled, subrequests of the same index will be routed to the same shard only in the following situations:
- Users don't customize the routing during writes.
- Users don't customize the `\_id` field for a single document.

In the above situations, the bulk request cannot be optimized because the optimization will conflict with the user-defined routing and `\_id`.

### Query limits
After the optimization is enabled, a random routing is automatically added for each subrequests of a bulk request. This doesn't affect general queries at all. However, it affects queries for getting a single document by ID (getById), because ES' current implementation of `getById` uses `\_id` to route shards by default. This problem also exists in the scenarios where users customize the routing during writes. In this case, `getById` can only get the original document information by carrying the correct routing at the same time, which can be obtained through ordinary queries.

### Scenario limits
This optimization item works better in scenarios where there are many nodes and each index has many shards. Its optimization effect may not be obvious in scenarios with a small number of nodes and a small number of shards per index, for example, less than 10 shards.

## Optimization Effect
Testing in online large customer clusters (with 100+ nodes and 100+ shards per index) shows that after the bulk routing optimization is enabled, the rejections are directly reduced to 0, the CPU utilization is decreased by 25%, and the write speed is increased by 10%.

## Supported Versions
6.8.2, 7.5.1, and 7.10.1

 
