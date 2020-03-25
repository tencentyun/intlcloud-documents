1. Execution Engine  
    Hive on Tencent Cloud Elastic MapReduce (EMR) currently supports three execution engines:
    - MR
    - TEZ
    - Spark

   Select TEZ, if needed, when you purchase an EMR cluster. Normally, TEZ is the recommended execution engine due to higher computing efficiency.

2. Storage  
    Currently, Tencent Cloud supports the following storage media: local data disk, HDD cloud disk, SSD cloud disk, and COS (most cost-efficient).

3. Data format  
    Tencent Cloud supports multiple compression algorithms such as Snappy and LZO. You are recommended to format your files in ORC or Parquet for greater space utilization and computing efficiency in Hive.

4. How to choose the best query engine?  
    Currently, EMR supports SQL-based query engine Presto, SparkSQL, and Hive. Presto allows you to query a variety of data sources, while SparkSQL is good for applications that require low-latency. For querying general data warehouse, use Hive + TEZ.

5. Data security  
    If you use COS as underlying storage, external tables are recommended to prevent the data from being accidentally deleted; if your data is stored in HDFS, you are recommended to enable the HDFS Recycle Bin to recover the deleted data.
