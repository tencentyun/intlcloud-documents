Flink is an open-source distributed, high-performance, highly available, and accurate data stream execution engine. It provides diverse features such as data distribution, data communication, and fault tolerance for distributed computations over data streams. Based on the stream execution engine, Flink provides APIs at a higher abstraction layer for you to write distributed jobs.
- Distributed: Flink can run on multiple machines.
- High-performance: Flink has a high processing performance.
- Highly available: Flink supports an automatic application restart mechanism.
- Accurate: Flink can ensure the accuracy of data processing.
![](https://qcloudimg.tencent-cloud.cn/raw/4244dee1e4e174671be9691f4b0a833d.png)

As shown in the figure, the data source on the left contains real-time logs or data in the database, file system, or key-value storage system. Flink in the middle organizes the data and outputs the computed data to the destination on the right, which can be an application system or storage system. In summary, Flink has three core components:
- Data source: The data source on the left.
- Transformations: Operators, which process data.
- Data sink: Output component, which outputs the computed data to other application systems.

## Use cases
Flink has the following three use cases:
1. Event-driven applications
An event-driven application is stateful. It ingests data from one or more event streams and triggers computations, status updates, or external actions based on the events.
![](https://qcloudimg.tencent-cloud.cn/raw/b7a975d173fbdd7bfeb7c58a8e48710d.png)
In a traditional architecture (left), an application needs to read/write data from/to a remote transactional database, such as MySQL. For an event-driven application, data and computation are co-located. The application only needs to access the local memory or disk to get data, so it delivers a higher throughput and lower latency.
  - Flink supports event-driven applications by virtue of the following features:
  - Efficient status management: Flink comes with state backends, which store the intermediate status information.
  - Rich windows: Flink has tumbling, sliding, and other windows.
  - Various notions of time: Flink supports event time, processing time, and ingestion time.
Flink supports "at-least-once" and "exactly-once" fault tolerance levels.
2. Real-time data analytics applications
Analytical jobs extract valuable information and metrics from raw data. Traditionally, batch queries are used, or events are recorded to form an application based on the limited data set. To get the analysis result of the latest data, this mode needs to add the data to the data set, perform the query or run the application again, and write the result to a storage system or generate a report.
![](https://qcloudimg.tencent-cloud.cn/raw/d34e6d5c91e06f1007048f8603f0b64a.png)
3. Real-time data warehouse and ETL
Extract, Transform, and Load (ETL) is a process that extracts, transforms, and loads data in a business system to a data warehouse.
In traditional mode, the offline data warehouse centrally stores business data and performs ETL and runs other models at regular intervals based on the fixed computing logic to generate reports. It mainly builds T+1 offline data, pulls incremental data every day through periodic jobs, creates topic-level data related to different businesses, and provides the T+1 data query API externally.
![](https://qcloudimg.tencent-cloud.cn/raw/3155fa232c7b3606fe03463a3e991b9d.png)
The above figure compares the offline data warehouse ETL and real-time data warehouse. As can be seen, the offline mode is inferior in terms of computing and data real-timeness. Data becomes less valuable over time and needs to reach the user as soon as possible; therefore, real-time data warehouses are demanded.
For more information on API layers, see the following documents:
![](https://qcloudimg.tencent-cloud.cn/raw/be0341eab77eff82fb111f879b25a5c5.png)
  - [Table API & SQL](https://nightlies.apache.org/flink/flink-docs-release-1.9/dev/table/): The Table API is tightly integrated with the DataSet or DataStream. You can create a table through a DataSet or DataStream and convert it into a DataSet or DataStream through operations such as FILTER, SUM, JOIN, and SELECT. The SQL API is based on Apache Calcite at the underlying layer and is more flexible than other APIs, as Apache Calcite implements the SQL standard to allow for the direct use of SQL statements. The Table API and SQL API can work together as both of them return table objects.
  - [DataStream API](https://nightlies.apache.org/flink/flink-docs-release-1.9/dev/datastream_api.html) and [DataSet API](https://nightlies.apache.org/flink/flink-docs-release-1.9/dev/batch/): They mainly process streaming data and batch data and encapsulate lower-level APIs to support higher-order functions such as FILTER, SUM, MAX, and MIN. They are easy to use and popular in actual applications.
  - [Stateful Stream Processing](https://nightlies.apache.org/flink/flink-docs-release-1.9/dev/api_concepts.html): It provides time- and status-based control and is a bit complex and hard to use. It mainly applies to the logic of complex event processing.

## Environment information
- By default, Flink is deployed on the master and core nodes in a cluster. It is an out-of-the-box service.
- After logging in, you can run the `su hadoop` command to switch to the `hadoop` user and then perform local tests.
- The Flink software path is `/usr/local/service/flink`.
- The log path is `/data/emr/flink/logs`.

For more information, see the [community documentation](https://flink.apache.org/).