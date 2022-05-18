## Overview

DataHub is a data access and processing platform in Tencent Cloud, which provides data access, processing, and distribution features at one stop. Data is vital in internet businesses, and data access and reporting serve as the bridge between data generation, computing, storage, and analysis throughout the entire linkage. Therefore, simple yet efficient data access is critical. A business usually has data to be reported to the backend for storage, analysis, computing, and search, such as business metrics, process information, and monitoring data. The general processing linkage is as shown below:

![](https://qcloudimg.tencent-cloud.cn/raw/66b42d8592956e8e96883253a34175ef.png)

You can set up a classic data reporting architecture generally in the following steps:

1. Build/Purchase a storage engine to store reported data.
2. Develop and deploy a server to receive data, define APIs, and run the service.
3. Define information such as API protocol and authentication on the client and server.
4. Write code based on the protocol information for the client to report data.

In the above four steps, the development and deployment workload for the server is the highest, as you need to consider code logic development as well as the scalability and stability of the server and downstream storage. In addition, when the data volume gets high, problems on the server will become more obvious, and the server needs to be maintained with a lot of manpower and resources. As tasks involved in this regard are generally universal, DataHub aims to meet the requirements in such scenario by offering a stable, elastic, high-reliability, and high-throughput data access service.

## How It Works

DataHub provides SDKs for various programming languages, including Java, Python, Go, PHP, Node.js, C++, and .NET, to help the client better report data. Data can be reported to a storage engine such as CKafka in three simple steps (more Tencent Cloud message queue services like TDMQ for RocketMQ, Pulsar, RabbitMQ, and CMQ will be supported in the future).

  1. Create an access point in the DataHub console.
  2. Report the data via the SDK.
  3. Query the data.

## Directions

1. Create an access point in the DataHub console as instructed in [Reporting over HTTP](https://intl.cloud.tencent.com/document/product/597/46807).
2. Report the data via the SDK as instructed in [Data Reporting SDK](https://intl.cloud.tencent.com/document/product/597/46808).
3. Query the data. After the data is reported to DataHub, you can query the message content in real time as instructed in [Querying Message](https://intl.cloud.tencent.com/document/product/597/39719).

## Data Empowerment

After you complete data access easily and quickly through DataHub, how to make the data generate value becomes the most important thing. To address this, DataHub provides two core features:

### Data processing

DataHub offers a simple data ETL engine, which can cleanse most types of data in order to simply format and process data for subsequent use.

### Data distribution

   After data processing is completed, DataHub can also meet the data distribution needs in various scenarios:

   - Real-time search: When you need to search for data, you can export real-time data streams to a search service such as Elasticsearch and CLS.
   - OLAP analysis: When you need to analyze data, you can export real-time data streams to an engine such as ClickHouse and TDW.
   - Persistent storage: When you need to persistently store data, you can export real-time data streams to a persistent storage engine such as HDFS and COS.
   - Stream computing: When you need to process data with custom code, you can use Flink, Spark, and code in different programming languages over the standard Kafka protocol for data processing.

After the data has gone through the four stages of reporting, access, processing, and distribution, the general data reporting and analysis needs can be easily and quickly satisfied, creating data value at ultra low costs.
