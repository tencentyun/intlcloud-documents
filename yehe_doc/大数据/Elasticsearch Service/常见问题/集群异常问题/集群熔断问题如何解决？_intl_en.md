## Circuit Breaking Overview
ES provides a variety of official circuit breakers to prevent ES cluster errors caused by OutOfMemoryError when the memory utilization is too high. It is equipped with various types of child circuit breakers to specify the limit on memory available to specific requests. In addition, there is a parent circuit breaker that is used to specify the total amount of memory available across all child circuit breakers.
>? Circuit breaking indicates that the current node's JVM utilization is too high, so the circuit breaker is triggered to prevent OOM. At this point, you can reduce the load of the node by appropriately reducing reads/writes, freeing up the memory, etc. You can also increase the size of the JVM by upgrading the node's memory specification.

## Common Memory Cleanup Methods
- Clear field data cache: when you perform aggregation and sorting operations on fields of `text` type, the data structure called `fielddata` will be used, which may take up a lot of memory. You can view the memory utilization of field data in an index by running the following command in the **Dev Tools** on the Kibana page:
```
GET /_cat/indices?v&h=index,fielddata.memory_size&s=fielddata.memory_size:desc
```
If field data takes up a lot of memory, you can clear it by running the following command in the **Dev Tools** on the Kibana page:
```
POST /${Indexes whose fielddata takes up a lot of memory}/_cache/clear?fielddata=true
```
- Clear segments: the FST structure of each segment will be loaded into the memory, which will not be recycled by GC. Therefore, a large number of segments in an index will also result in a high memory utilization. You can view the number of segments per node and the amount of memory used by them by running the following command in the **Dev Tools** on the Kibana page:
```
GET /_cat/nodes?v&h=segments.count,segments.memory&s=segments.memory:desc
```
If segments take up a too large amount of memory, you can delete indexes that are not used, close indexes, or regularly merge indexes that are no longer updated.
- Scale out the cluster: if the circuit breaker is still triggered frequently after you clean up the memory, your cluster size may be no longer suitable for your business, and we recommend you scale it out. For more information, please see [Adjusting Configuration](https://intl.cloud.tencent.com/document/product/845/30944).

## Circuit Breaker List
### Elasticsearch's official circuit breakers
- Parent circuit breaker
The parent circuit breaker limits the total amount of memory used by all child circuit breakers. When it is triggered, the possible log information is as follows:
```
Caused by: org.elasticsearch.common.breaker.CircuitBreakingException: [parent] Data too large, data for [<transport_request>] would be [1749436147/1.6gb], which is larger than the limit of [1622605824/1.5gb], real usage: [1749435872/1.6gb], new bytes reserved: [275/275b]
```
- Field data breaker
When you perform aggregation and sorting operations on fields of `text` type, the "fielddata" data structure will be generated. The field data breaker estimates how much data is loaded into the memory. When the memory usage by the estimated data reaches its threshold, it will be triggered. The possible log information is as follows:
```
org.elasticsearch.common.breaker.CircuitBreakingException: [fielddata] Data too large, data for [_id] would be [943928680/900.2mb], which is larger than the limit of [255606128/243.7mb]
```
- In flight requests circuit breaker
The in flight requests circuit breaker limits the memory usage of all currently active incoming requests at the transport or HTTP level. When it is triggered, the possible log information at this time is as follows:
```
[o.e.x.m.e.l.LocalExporter] [1611816935001404932] unexpected error while indexing monitoring document
org.elasticsearch.xpack.monitoring.exporter.ExportException: RemoteTransportException[[1611816935001404732][9.10.153.16:9300][indices:data/write/bulk[s]]]; nested: CircuitBreakingException[[in_flight_requests] Data too large, data for [<transport_request>] would be [19491363612/18.1gb], which is larger than the limit of [17066491904/15.8gb]];
```

### ES' proprietary circuit breaker
One of the drawbacks of Elasticsearch's official circuit breaking mechanism is that only those requests that are often problematic are tracked to estimate the memory utilization, making it impossible to limit the amount of memory available to requests or trigger a circuit breaker based on the actual memory utilization on the current node. ES has a proprietary circuit breaker to address this problem with JVM Old memory utilization.

This circuit breaker monitors the JVM Old memory utilization. When the utilization exceeds `85%`, write requests will be rejected. If GC still cannot recycle the JVM Old memory, query requests will be rejected when the utilization reaches `90%`. If a request is rejected, the client will receive the following response:
```
{
    "status": 403,
    "error": {
        "root_cause": [{
            "reason": "pressure too high, (smooth) bulk request circuit break",
            "type": "status_exception"
        }],
        "type": "status_exception",
        "reason": "pressure too high, (smooth) bulk request circuit break"
    }
}
```
