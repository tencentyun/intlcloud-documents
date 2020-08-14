Elasticsearch provides multiple circuit breakers to prevent ES cluster errors caused by OutOfMemoryError when the memory utilization is too high. It is equipped with various types of child circuit breakers to specify the limit on memory available to specific requests. In addition, there is a parent circuit breaker that is used to specify the total amount of memory available across all child circuit breakers.

### ES Circuit Breakers

One of the drawbacks of Elasticsearch circuit breaker mechanism is that only those requests that are often problematic are tracked to estimate the memory utilization, making it impossible to limit the amount of memory available to requests or trigger a circuit breaker based on the actual memory utilization on the current node. ES has a proprietary circuit breaker to address this problem with JVM OLD memory utilization.

This circuit breaker monitors the JVM OLD memory utilization. When the utilization exceeds `85%`, write requests will be rejected. If GC still cannot recycle the JVM OLD memory, query requests will be rejected when the utilization reaches `90%`. If a request is rejected, the client will receive the following response:
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

The above error message indicates that the JVM OLD memory is currently heavily loaded and you need to free up some memory in JVM before retrying.

### Common Methods to Free up Memory

* Clear fielddata cache: When you perform aggregation and sorting operations on fields of text type, the data structure called fielddata will be used, which may take up a lot of memory. You can view the memory utilization of the fielddata in an index by running the following command in the **Dev Tools** on the Kibana page:
    ```
    GET /_cat/indices?v&h=index,fielddata.memory_size&s=fielddata.memory_size:desc
    ```
   If fielddata takes up a lot of memory, you can clear it by running the following command in the **Dev Tools** on the Kibana page:
    ```
    POST /${Indices whose fielddata takes up a lot of memory}/_cache/clear?fielddata=true
    ```
* Clear segments: The FST structure of each segment will be loaded into the memory, which will not be recycled by GC. Therefore, a large number of segments in an index will also result in a high memory utilization. You can view the number of segments per node and the amount of memory used by them by running the following command in the **Dev Tools** on the Kibana page:

    ```
    GET /_cat/nodes?v&h=segments.count,segments.memory&s=segments.memory:desc
    ```
    If segments take up a too large amount of memory, you can delete indices that are not used, close indices, or regularly merge indices that are no longer updated.

* Scale out your cluster: If the circuit breaker is still triggered frequently after you clean up the memory, your cluster size may be no longer suitable for your business, and you are recommended to scale it out. For more information, see [Scaling out a Cluster](https://intl.cloud.tencent.com/document/product/845/30944).
