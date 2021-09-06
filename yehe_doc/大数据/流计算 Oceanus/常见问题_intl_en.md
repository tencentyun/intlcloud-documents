### What is real-time stream data?

When users browse the web or use apps, their operation behaviors will continuously be aggregated into logs. When gamers play games, a steady stream of operation records will also be generated. Such continuously generated data is real-time stream data. By understanding this type of data, you can monitor your business in real time and quickly discover new opportunities.

### What are the advantages of stream computing over batch computing?

Batch computing requires the collection of all data before starting various complex computations which may last from hours to one day. Stream computing processes stream data in quasi-real time, without requiring full data collection, which is beneficial to real-time business monitoring and new opportunity discovery.

### What is a CU?

A compute unit (CU) is the smallest unit of computing resources provided by Oceanus, which contains 1 CPU core and 4 GB memory. 



### Can the JAR job mode be connected to self-built services?

Yes. You can access your self-built services such as Druid and Kafka through peering connection.

### What are fine-grained resources?
Fine-grained resources refer to resources whose computing resource unit specifications can be below 1 CU (1 CPU core and 4 GB memory). Oceanus currently supports three types of CU specifications: 0.5 CU, 1 CU, and 2 CU. Different specifications can be set for JobManager and TaskManager, respectively.

### Why does the actual running job concurrency fail to reach the maximum job concurrency?
In the process of using fine-grained resources in resource configuration, there is a very small probability that resource fragments may affect job operations, so the actual running job concurrency may not reach the maximum job concurrency. You can avoid resource fragments as much as possible by choosing an appropriate resource specification. If the above issue occurs, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
