## 什么是熔断
Elasticsearch Service 提供了多种官方的熔断器（circuit breaker），用于防止内存使用过高导致 ES 集群因为 OutOfMemoryError 而出现问题。Elasticsearch 设置有各种类型的子熔断器，负责特定请求处理的内存限制。此外，还有一个父熔断器，用于限制所有子熔断器上使用的内存总量。
>? 出现熔断说明当前节点 JVM 使用率过高，通过熔断保护进程不会 OOM。此时可以通过适当降低读写、清理内存等方法降低节点负载，也可以通过升级节点内存规格来提高 JVM 大小。

## 常用的内存清理方法
- 清理 fielddata cache：在 text 类型的字段上进行聚合和排序时会使用 fileddata 数据结构，可能占用较大内存。可以在 Kibana 界面的【Dev Tools】中使用如下命令查看索引的 fielddata 内存占用：
```
GET /_cat/indices?v&h=index,fielddata.memory_size&s=fielddata.memory_size:desc
```
若 fielddata 占用内存过高，可以在 Kibana 界面的【Dev Tools】中使用如下命令清理 fielddata：
```
POST /${fielddata占用内存较高的索引}/_cache/clear?fielddata=true
```
- 清理 segment：每个 segment 的 FST 结构都会被加载到内存中，并且这些内存是不会被 GC 回收的。因此如果索引的 segment 数量过大，也会导致内存使用率较高。可以在 Kibana 界面的【Dev Tools】中使用如下命令查看各节点的 segment 数量和占用内存大小：
```
GET /_cat/nodes?v&h=segments.count,segments.memory&s=segments.memory:desc
```
若 segment 占用内存过高，可以通过删除部分不用的索引、关闭索引，或定期合并不再更新的索引等方式缓解。
- 扩容集群：如果您清理内存后，仍频繁触发熔断，说明您的集群规模已经不匹配于您的业务负载，最好的方式是扩大集群规模，具体可参考 [扩容集群](https://intl.cloud.tencent.com/document/product/845/30944)。

## 熔断器介绍
### Elasticsearch 官方熔断器
- 父熔断器（Parent circuit breaker）
父熔断器限制所有子熔断器上使用的内存总量，当触发父熔断器熔断时，可能的日志信息如下：
```
Caused by: org.elasticsearch.common.breaker.CircuitBreakingException: [parent] Data too large, data for [<transport_request>] would be [1749436147/1.6gb], which is larger than the limit of [1622605824/1.5gb], real usage: [1749435872/1.6gb], new bytes reserved: [275/275b]
```
- Field data 熔断器（Field data breaker）
当对 text 字段聚合或排序时，会产生 Field data 数据结构。Field data 熔断器会预估有多少数据被加载到内存中。当预估的数据占用内存到达 Field data 熔断器阈值时，会触发 Field data 熔断器熔断。此时可能的日志信息如下：
```
org.elasticsearch.common.breaker.CircuitBreakingException: [fielddata] Data too large, data for [_id] would be [943928680/900.2mb], which is larger than the limit of [255606128/243.7mb]
```
- In flight 请求熔断器（In flight requests circuit breaker）
In flight 请求熔断器限制了在 transport 和 HTTP 层的所有当前传入的请求所使用的内存。当触发 In flight 请求熔断器时，可能的日志信息如下：
```
[o.e.x.m.e.l.LocalExporter] [1611816935001404932] unexpected error while indexing monitoring document
org.elasticsearch.xpack.monitoring.exporter.ExportException: RemoteTransportException[[1611816935001404732][9.10.153.16:9300][indices:data/write/bulk[s]]]; nested: CircuitBreakingException[[in_flight_requests] Data too large, data for [<transport_request>] would be [19491363612/18.1gb], which is larger than the limit of [17066491904/15.8gb]];
```

### 腾讯云 ES 自研熔断器
官方熔断机制的一个不足是仅跟踪那些经常会出问题的请求来预估内存的使用，而无法根据当前节点的实际内存使用状态，来限制请求的内存使用或触发熔断。在腾讯云 ES 中，开发了针对 JVM OLD 区内存使用率的自研熔断器来解决这个问题。

腾讯云 ES 的自研熔断器监控 JVM OLD 区的使用率，当使用率超过`85%`时开始拒绝写入请求，若 GC 仍无法回收 JVM OLD 区中的内存，在使用率到达`90%`时将拒绝查询请求。当请求被拒绝时，客户端将收到如下的响应：
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
