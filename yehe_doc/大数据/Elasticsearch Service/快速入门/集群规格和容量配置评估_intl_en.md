Tencent Cloud Elasticsearch Service (ES) is a distributed multi-node cluster, where each node consists of computing and storage components. This document provides guidance on how to select an appropriate ES configuration based on your business needs in some common use cases. These suggestions are for your reference and should be adjusted according to your actual business conditions. The auto scaling mechanism provided by ES allows you to scale out your cluster at any time to get optimal cluster specifications when performance bottlenecks occur as your business grows.

## Storage Capacity Estimation
The storage capacity of ES is mainly affected by the following factors:
- Number of replicas: replicas can improve data reliability but also increase storage costs. The default and recommended number of replicas is 1, and for some scenarios where the data loss caused by exceptions is tolerable, you can consider setting the number of replicas to 0.
- Data expansion: in addition to raw data, ES also needs to store indices and columnar data, and the data size generally expands by 10% after technologies such as encoding and compression are applied.
- Internal task overheads: ES occupies approximately **20%** of the disk space, which is used for segment merges, ES Translog, logs, etc.
- OS reserve: Linux reserves 5% of the disk space for root users by default for key process handling, system restoration, and disk defragmentation.

Therefore, the actual space occupied by data in ES can be estimated with the following formula:
``` 
Actual space = source data * (1+ number of replicas) * (1 + data expansion) / (1 - internal task overheads) / (1 - OS reserve)
        ≈ source data * (1 + number of replicas) * 1.45
```
To ensure the stable operations of the service, we recommend you reserve at least 15% of the disk space. Therefore, the recommended disk capacity is:
``` 
Storage capacity = source data * (1 + number of replicas) * 1.45 * (1 + reserved space)
        ≈ source data * (1 + number of replicas) * 1.67
```
Generally, to ensure the performance and stability of your cluster, we recommend that the ratio of memory to disk capacity not exceed the following limit:
- For hot data, the recommended ratio of memory to disk capacity is 1:96.
- For warm data, the recommended ratio of memory to disk capacity is 1:480.

>! ES is widely used in various scenarios such as log, website search, metrics, and APM. The above storage capacity estimation method is general, and you can highly optimize ES based on your own needs to reduce your storage costs.


## Computing Resource Estimation
ES computing resources are mainly consumed in the write and query processes, and the complexity of writes and queries and their proportion vary by business scenario; therefore, computing resources are more difficult to estimate than storage resources. However, storage resources generally become a bottleneck earlier, so we recommend you estimate the storage capacity first, and then preliminarily select computing resources and check whether they are sufficient in the testing process.

The following provides guidance on how to estimate computing resources in several common use cases:
- Log scenario: log is a typical scenario involving more writes than reads, and computing resources are mainly consumed in the write process. Our experience in log scenarios shows that 2 CPU cores and 8 GB memory can sustain up to 5,000 writes per second, subject to the actual business scenario. As instance performance is generally scaled linearly with the total amount of computing resources, you can estimate the write capacity based on the total amount of instance resources; for example, 8 CPU cores and 32 GB memory can sustain up to 20,000 writes per second.
- Structured data scenarios such as metrics and APM: these scenarios also involve more writes than reads but consume less computing resources than log scenarios; for example, 2 CPU cores and 8 GB memory generally can sustain 10,000 writes per second. You can estimate the actual write capacity of instances with different specifications by using the linear scaling method as described in the log scenario.
- Search scenarios such as website search and application search: these scenarios involve more reads than writes, and computing resources are mainly consumed in the query process. As the query complexity varies significantly by use case, computing resources are the most difficult to estimate. We recommend you preliminarily select computing resources based on storage resources and then perform verification and make adjustments in the testing process.


## Instance Type Selection and Testing
After estimating storage and computing resources, you can preliminarily select the instance type, including the node specification and the number of nodes. We recommend you select the instance type as follows:
- We recommend you select at least 3 nodes to prevent split-brain problems in your ES instance and ensure its high node fault tolerance.
>?Split-Brain: a problem where both nodes believe that they are the only active server and thus scramble for resources.
>
- If you need a high storage capacity, we recommend you select high-specced nodes rather than high numbers of low-specced nodes, as this benefits the performance and stability of large instances significantly. For example, if you need 40 CPU cores, 160 GB memory, and 5 TB storage capacity, we recommend you select a 5-node instance with 8 CPU cores, 32 GB memory, and 1 TB storage capacity each. Likewise, when you need to scale out your instance, we recommend you perform vertical scaling first to expand the node capacity to 8 CPU cores and 32 GB memory or 16 CPU cores and 64 GB memory and then consider horizontal scaling to increase the number of nodes.
- After you preliminarily select the instance type, you can test it by using real data and observe monitoring information such as CPU utilization, write metrics (performance and rejection rate), and query metrics (QPS and rejection rate) to further verify whether the instance type is appropriate. In addition, we recommend you configure alarms for the above monitoring information, so that you can promptly identify issues such as resource insufficiency.


## Estimation of Number of Shards
Each ES index is split into multiple shards, and data is distributed among different shards according to the hash algorithm. As the number of an index's shards affects the read/write performance and failure recovery speed and usually cannot be easily changed, it needs to be considered in advance. We recommend you configure the number of shards as follows:
- The recommended size of a single shard is 10–50 GB, and you can preliminarily determine the number of an index's shards based on this value. Shards should be neither too large nor too small. If they are too large, ES failure recovery may be slow; if they are too small, there may be many shards, and each shard uses certain amounts of CPU and memory resources, which may cause various issues, including poor read/write performance and memory insufficiency.
- During testing, you can appropriately adjust the number of shards based on the actual size of each index and expected future growth.
- When the number of shards exceeds the number of data nodes, we recommend you adjust the former to make it close to an integer multiple of the latter, so that the shards can be evenly distributed among all the data nodes.
- For log and metric scenarios, we recommend you use the [rollover index](https://www.elastic.co/guide/en/elasticsearch/reference/master/indices-rollover-index.html) feature of ES to generate new indices on a rolling basis, so that you can promptly adjust the number of shards when you find that the shard size is unreasonable.

For example, if an instance has 5 data nodes and the current index size is 150 GB and is expected to grow by 50% in half a year, and you set the size of each shard to 30 GB, then you need 150 GB * (1 + 50%) / 30 ≈ 7 shards. Considering that two of the data nodes sustain 2/7 of the data and the data is unevenly distributed among the nodes, you can adjust the number of shards to 10.

