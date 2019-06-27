ES is provided in the form of distributed multi-node clusters. Each node has two parts: computation and storage. Below are some fact-based suggestions on how to choose the appropriate configuration according to your business needs in common application scenarios. They are for your reference only, and you are recommended to gradually explore the optimal options during the actual use of the service. ES features an elastic scaling mechanism, enabling you to scale the clusters to break the performance bottleneck as your business grows.

## Storage Capacity Estimation
The main factors affecting the storage capacity of ES are as follows:

- Number of replicas: Replicas help improve the data reliability but increase the storage costs at the same time. The default (and recommended) number of replicas is 1. In certain scenarios where you can withstand data losses caused by exceptions, you can even set this number to 0.
- Data expansion: In addition to the original data, ES needs to store indices and column data, which generally leads to a data expansion of 10% after techniques such as encoding and compression are applied.
- Internal task overheads: ES occupies approximately **20%** of disk capacity for consolidated segments, ES translogs, and logs.
- OS reservation: The Linux OS reserves 5% of disk capacity for the root user by default for critical process handling, system recovery, and prevention of disk fragmentation.

Therefore, the actual capacity occupied by the data in ES can be estimated by the following formula:

``` 
Actual capacity = source data * (1 + number of replicas) * (1 + data expansion) / (1 - internal task overheads) / (1 - OS reservation)
        ≈ Source data * (1 + number of replicas) * 1.45
``` 
To ensure stable operations of the service, it is recommended to reserve at least 50% of the storage capacity. Therefore, the recommended storage capacity to be applied for is:
``` 
Storage capacity = Source data * (1 + number of replicas) * 1.45 * (1 + reserved capacity)
        ≈ Source data * (1 + number of replicas) * 2.2
``` 

> **Note:**
> ES is widely used in scenarios such as logging, site retrieval, metrics, and APM. The storage capacity estimation method above is quite generalized. You can deeply optimize ES according to your actual needs to reduce storage costs.


## Computing Resource Estimation
In ES, computing resources are mainly consumed in the process of writing and querying, and the complexity and proportion of writing and querying vary by businesses, making computing resources more difficult to estimate than storage resources. However, in general, storage resources will become a bottleneck first, so it is recommended that you estimate the storage resources first and then select computing resources as instructed in [ES Node Type](https://cloud.tencent.com/product/es/cluster-node). After that, you can check whether the computing resources are sufficient during the testing process. Below are some best practices for estimating the computing resources in common application scenarios:

- Logging scenarios: In logging scenarios, there are more writes than reads, and the computing resources are mainly consumed during the writing process. Our experience with such scenarios is that 2 cores and 8 GB memory can support up to 5,000 writes per second. Please note that this number may vary in different businesses. Basically, since the performance of an instance is linearly increased with the total amount of computing resources, you can estimate the write capacity by the total amount of instance resources. For example, 6 cores and 24 GB memory can support up to 15,000 writes per second, and 40 cores and 160 GB memory can support up to 100,000 writes per second.
- Structured data scenarios such as metrics and APM: In these scenarios, there are also more writes than reads, but the consumption of computing resources is lower than that in logging scenarios. 2 cores and 8 GB memory can generally support 10,000 writes per second. You can evaluate the actual write capacity of different instance specifications in the same way as described in the logging scenarios above.
- Search scenarios such as site search and application search: In these scenarios, there are more reads than writes, and the computing resources are mainly consumed in the querying process. As the querying complexity varies significantly by application scenarios, the computing resources are the most difficult to estimate in this case. It is recommended that you select the computing resource based on the storage resources first and then verify their sufficiency and adjust them during the testing process.


## Instance Type Selection and Testing

After estimating the storage and computing resource, you can choose an appropriate instance type as instructed in [ES Node Type](https://cloud.tencent.com/product/es/cluster-node), which includes two parts: node specifications and node quantity. Below are general recommendations for choosing an instance type:

- Select at least 3 nodes to avoid the risk of split-brain in the ES instance and ensure high node fault tolerance.
- If you need very high storage capacity, instead of selecting many low-spec nodes, you are recommended to select a few high-spec nodes to enjoy higher instance performance and stability. For example, if you need 40 cores, 160 GB memory, and 5 TB storage capacity, you are recommended to select an instance consisting of five nodes of 8 cores, 32 GB memory, and 1 TB storage capacity each. For the same reason, when you need to scale the instance, you are recommended to scale up from 8 core and 32 GB memory to 16 cores and 64 GB memory first before considering scale-out.
- After you preliminarily select the instance type, you can test the instance with real data and further check whether it is suitable for your business by observing monitoring metrics such as CPU utilization, writes (performance and rejection rate), and queries (QPS and rejection rate). In addition, you are recommended to configure alarms for these metrics to help identify issues such as insufficient resources during actual use of the service.


## Shard Quantity Estimation

Each ES index is divided into multiple shards, and data is broken down for storage in different shards based on the hash algorithm. As the number of index shards affects read/write performance and failover speed and is hard to change, it needs to be planned well in advance. Here are some suggestions on how to determine the number of shards:

- It is recommended that the size of a single shard be between 10 and 50 GB. You can determine the number of shards for the index based on this. Shard size should not be too large or too small. If too large, it may slow down failover in ES; if too small, it may result in too many shards and lead to problems such as constrained read/write performance and insufficient memory as every shard needs to use a certain amount of CPU and memory resources.
- During the testing process, the number of shards can be appropriately adjusted according to the actual size of each index and the expected growth.
- If the number of shards is higher than the number of data nodes, it is recommended that the former be close to an integer multiple of the latter, so that the shards can be evenly distributed across all data nodes.
- For scenarios such as logging and metrics, it is recommended to use the [Rollover Index](https://www.elastic.co/guide/en/elasticsearch/reference/master/indices-rollover-index.html) feature that comes with ES to continuously produce new indices on a rolling basis. This also makes it easy to adjust the number of shards promptly if you find the shard size unreasonable.

For example, suppose that an instance has 5 data nodes, and the current size of the indices is 150 GB, which is expected to increase by 50% in six months. If each shard is set to be 30 GB, about 150 GB * (1 + 50%) / 30 ≈ 7 shards are needed. Considering that there are two data nodes that support 2/7 of the data pressure, the pressure is not evenly distributed among the nodes, so it is recommended to adjust the number of shards to 10.
