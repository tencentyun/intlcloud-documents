Elastic MapReduce (EMR) clusters supports many application scenarios by running big data frameworks Hadoop and Spark. Below are some typical EMR application scenarios:
## Offline Data Analysis
EMR synchronizes vast amounts of log data from business applications (e.g. games, webs, and mobile Apps) servers to nodes or COS. With Hue, an open source SQL Workbench for Data Warehouses, you can use big data frameworks such as Hive, Spark, and Presto to analyze data to derive business insights. In addition, you can use Sqoop to integrate and analyze the data scattered across TencentDB and other storage engines. Sqoop synchronizes the analyzed data back to TenentDB to support data visualization services like RayData.
![](https://main.qcloudimg.com/raw/d812bdff23ff21fd83f44183bf6724c2.png)
## Streaming Data Processing
After pushing the real-time data generated from business servers to the CMQ messaging middleware through APIs and SDKs in programs/tools, you can select an appropriate streaming data processing engine in EMR to analyze the data for real-time alarming in respond to business changes. The analysis results can be synced to storage engines such as TencentDB in real time, which helps you monitor your business by using data visualization services like RayData.
![](https://main.qcloudimg.com/raw/e9d300b266f96cfc1083533a22318bb2.png)
## COS Data Analysis
You can use EMR to process and analyze vast amounts of data stored in COS so that computation and storage can be completely separated. This architecture allows you to use various data synchronization tools in COS. At the same time, you can use multiple Hadoop cluster versions to analyze the same data to achieve data consistency and resolve legacy issues caused by the coexistence of multi-version Hadoop clusters.
![](https://main.qcloudimg.com/raw/cedc599e6f6ae54c255ecb641304a779.png)
