## Oceanus Overview  

Oceanus is a powerful real-time analysis tool in the big data ecosystem. With it, you can easily build various applications in just a few minutes, such as website clickstream analysis, targeted ecommerce recommendation, and IoT. Oceanus is developed based on Apache Flink and provides fully managed cloud services, so you don't need to care about the Ops of infrastructure. It can also be connected to data sources in the cloud for a complete set of supporting services.

Oceanus comes with a convenient console for you to write SQL analysis statements, upload and run custom JAR packages, and manage jobs. Based on the Flink technology, it can achieve a sub-second processing latency in datasets at the petabyte level.

This document describes how to connect Oceanus to COS. Currently, Oceanus is available in the dedicated cluster mode, where you can run various jobs and manage related resources in your own cluster.

## Prerequisites

#### Creating Oceanus cluster

Log in to the [Oceanus console](https://console.cloud.tencent.com/oceanus/workspace) and create an Oceanus cluster.

#### Creating COS bucket

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click **Create Bucket** to create a bucket as instructed in [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).
>? When you write data to COS, the Oceanus job must run in the same region as COS.
>

## Directions

Go to the [Oceanus console](https://console.cloud.tencent.com/oceanus/overview), create an SQL job, and select a cluster in the same region as COS.

#### 1. Create a source

```sql
CREATE TABLE `random_source` ( 
  f_sequence INT, 
  f_random INT, 
  f_random_str VARCHAR 
  ) WITH ( 
  'connector' = 'datagen', 
  'rows-per-second'='10',                  -- Number of date rows generated per second
  'fields.f_sequence.kind'='random',       -- Random number
  'fields.f_sequence.min'='1',             -- Minimum sequential number
  'fields.f_sequence.max'='10',            -- Maximum sequential number
  'fields.f_random.kind'='random',         -- Random number
  'fields.f_random.min'='1',               -- Minimum random number
  'fields.f_random.max'='100',             -- Maximum random number
  'fields.f_random_str.length'='10'        -- Random string length
);
```

>? Here, the built-in connector `datagen` is selected. Select a data source based on your actual business needs.
>

#### 2. Create a sink

```sql
-- Replace `<bucket name>` and `<folder name>` with your actual bucket and folder names.
CREATE TABLE `cos_sink` (
  f_sequence INT, 
  f_random INT, 
  f_random_str VARCHAR
) PARTITIONED BY (f_sequence) WITH (
    'connector' = 'filesystem',
    'path'='cosn://<bucket name>/<folder name>/',                 --- Directory path to which data is to be written
    'format' = 'json',                                       --- Format of written data
    'sink.rolling-policy.file-size' = '128MB',               --- Maximum file size
    'sink.rolling-policy.rollover-interval' = '30 min',      --- Maximum file write time
    'sink.partition-commit.delay' = '1 s',                   --- Partition commit delay
    'sink.partition-commit.policy.kind' = 'success-file'     --- Partition commit method
);
```

>? For more `WITH` parameters of a sink, see "Filesystem (HDFS/COS)".
>

#### 3. Configure the business logic

```sql
INSERT INTO `cos_sink`
SELECT * FROM `random_source`;
```

>! This is for demonstration only and has no actual business purposes.
>

#### 4. Set job parameters

Select `flink-connector-cos` as the **Built-in Connector** and configure the COS URL in **Advanced Parameters** as follows:

```shell
fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
fs.cosn.credentials.provider: org.apache.flink.fs.cos.OceanusCOSCredentialsProvider
fs.cosn.bucket.region: <COS region>
fs.cosn.userinfo.appid: <COS user appid>
```

The job is configured as follows:

- Replace `<COS region>` with your actual COS region, such as `ap-guangzhou`.
- Replace `<COS user appid>` with your actual `APPID`, which can be viewed in [Account Center](https://console.cloud.tencent.com/developer). 

>? For more information on job parameter settings, see "File System (HDFS/COS)".
>

#### 5. Start the job

Click **Save** > **Check Syntax** > **Release Draft**, wait for the SQL job to start, and go to the corresponding COS directory to view the written data.
