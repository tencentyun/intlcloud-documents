This document describes how to consume CLS logs with Flink in real time, analyze Nginx log data with Flink SQL, calculate web PVs/UVs, and write the result to self-built MySQL databases in real time.

**Components/Applications and their versions used in this document are as described below:**

| Technical Component     | Version                          |
|-----------|-----------------------------|
| Nginx     | 1.22                        |
| CLS   | -                           |
| Java      | OpenJDK version "1.8.0_232" |
| Scala     | 2.11.12                     |
| Flink SQL | Flink 1.14.5                |
| MySQL     | 5.7                         |

## Directions
### Step 1. Install the Tencent Cloud Nginx gateway
1. Purchase a CVM instance as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
2. Install Nginx as instructed in the directions for installing Nginx on Linux.
3. The installation is successful if you can access Nginx in the browser and see the following page:
![](https://qcloudimg.tencent-cloud.cn/raw/707ffb836a3af40d5cfcbaac25fda659.png)


### Step 2. Collect Nginx logs to CLS
1. Configure Nginx log collection as instructed in [Collecting and Searching NGINX Access Logs](https://intl.cloud.tencent.com/document/product/614/32939).
2. Install CLS's log collector LogListener as instructed in [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414). Similar to the open-source component Beats, LogListener is an agent that collects logs.
3. After index is enabled for log topics, you can query Nginx logs as shown below:

4. Enable [consumption over Kafka](https://intl.cloud.tencent.com/document/product/614/42752) in the CLS console to use the feature. You can consume a log topic as a Kafka topic. This document describes how to consume Nginx log data in real time with the stream computing framework Flink and then write the real-time computing result to MySQL.

### Step 3. Set up a MySQL database
For detailed directions, see [Creating MySQL Instance](https://intl.cloud.tencent.com/document/product/236/37785).
1. Log in to the database:
```
mysql -h 172.16.1.1 -uroot
```
2. Create the target database and table. Here, the `flink_nginx` database and `mysql_dest` table are created.
```
create database if not exists flink_nginx;
create table if not exists mysql_dest(
    ts timestamp,
    pv bigint,
    uv bigint
);
```

 

### Step 4. Deploy Flink
1. We recommend that you use the following versions for Flink deployment; otherwise, the installation may fail.
	- Purchase a CVM instance as instructed in [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
	- Install Scala 2.11.12 as instructed in [Ways to Install This Release](https://www.scala-lang.org/download/2.11.12.html).
2. Install Flink 1.14.15 and go to the SQL UI. Download the binary code package of Flink from the [Apache Flink website](https://flink.apache.org/downloads.html#apache-flink-1145) and start installation.
```
# Decompress the Flink binary package
tar -xf flink-1.14.5-bin-scala_2.11.tgz
cd flink-1.14.5

# Download Kafka dependencies
wget https://repo1.maven.org/maven2/org/apache/flink/flink-connector-kafka_2.11/1.14.5/flink-connector-kafka_2.11-1.14.5.jar
mv flink-connector-kafka_2.11-1.14.5.jar lib
wget https://repo1.maven.org/maven2/org/apache/kafka/kafka-clients/2.4.1/kafka-clients-2.4.1.jar
mv kafka-clients-2.4.1.jar lib

# Download MySQL dependencies
wget https://repo1.maven.org/maven2/org/apache/flink/flink-connector-jdbc_2.11/1.14.5/flink-connector-jdbc_2.11-1.14.5.jar
mv flink-connector-jdbc_2.11-1.14.5.jar lib
wget https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.11/mysql-connector-java-8.0.11.jar
mv mysql-connector-java-8.0.11.jar lib
wget https://repo1.maven.org/maven2/org/apache/flink/flink-table-common/1.14.5/flink-table-common-1.14.5.jar
mv flink-table-common-1.14.5.jar lib

# Start Flink
bin/start-cluster.sh
bin/sql-client.sh
```
3. The installation is successful if the following information is displayed. Note that the default web port is 8081.
![](https://qcloudimg.tencent-cloud.cn/raw/d988fff8bdbbdcaad4f4a2452d5c9ec1.png)
![](https://qcloudimg.tencent-cloud.cn/raw/24bafef62a5f676b28f72f0693f851f9.png)
 <img src="https://qcloudimg.tencent-cloud.cn/raw/964a9da5f694cbd8565001f058a5f52f.png" width="65%">

### Step 5. Consume CLS log data with Flink
1. On the SQL client UI, execute the following SQL statements:
```
-- Create a data source table to consume Kafka data
CREATE TABLE `nginx_source`
(
    `remote_user` STRING,           -- Field in the log, which indicates the client name.
    `time_local` STRING,            -- Field in the log, which indicates the local time of the server.
    `body_bytes_sent` BIGINT,       -- Field in the log, which indicates the number of bytes sent to the client.
    `http_x_forwarded_for` STRING,  -- Field in the log, which records the actual client IP when there is a proxy server on the frontend.
    `remote_addr` STRING,           -- Field in the log, which indicates the client IP.
    `protocol` STRING,              -- Field in the log, which indicates the protocol type.
    `status` INT,                   -- Field in the log, which indicates the HTTP request status code.
    `url` STRING,                   -- Field in the log, which indicates the URL.
    `http_referer` STRING,          -- Field in the log, which indicates the URL of the referer.
    `http_user_agent` STRING,       -- Field in the log, which indicates the client browser information.
    `method` STRING,                -- Field in the log, which indicates the HTTP request method.
    `partition_id` BIGINT METADATA FROM 'partition' VIRTUAL,    -- Kafka partition
    `ts` AS PROCTIME()                
)  WITH (
  'connector' = 'kafka',
  'topic' = 'YourTopic',  -- Topic name provided in the CLS console for consumption over Kafka, such as `out-633a268c-XXXX-4a4c-XXXX-7a9a1a7baXXXX` 
  'properties.bootstrap.servers' = 'kafkaconsumer-ap-guangzhou.cls.tencentcs.com:9096',   -- Service address provided in the CLS console for consumption over Kafka. The public network consumer address in Guangzhou region is used as an example. You need to enter the actual information.
  'properties.group.id' = 'kafka_flink', -- Kafka consumer group name
  'scan.startup.mode' = 'earliest-offset', 
  'format' = 'json',
  'json.fail-on-missing-field' = 'false', 
  'json.ignore-parse-errors' = 'true' ,
  'properties.sasl.jaas.config' = 'org.apache.kafka.common.security.plain.PlainLoginModule required username="your username" password="your password";',--Your username is the logset ID of the log topic, such as `ca5cXXXX-dd2e-4ac0-af12-92d4b677d2c6`, and the password is a string of your `secretid#secrectkey`, such as `AKIDWrwkHYYHjvqhz1mHVS8YhXXXX#XXXXuXtymIXT0Lac`. Note that `#` is required. We recommend that you use a sub-account key and follow the principle of least privilege when authorizing a sub-account, that is, configure the minimum permission for `action` and `resource` in the access policy of the sub-account.
  'properties.security.protocol' = 'SASL_PLAINTEXT',
  'properties.sasl.mechanism' = 'PLAIN'

);

--- Create the target table and write it to MySQL
CREATE TABLE `mysql_dest`
(
    `ts` TIMESTAMP,  
    `pv` BIGINT, 
    `uv` BIGINT 
)  WITH (
    'connector' = 'jdbc',
    'url' = 'jdbc:mysql://11.150.2.1:3306/flink_nginx?&amp;serverTimezone=Asia/Shanghai', -- Note the time zone settings here
    'username'= 'username',     -- MySQL account
    'password'= 'password',     -- MySQL password
    'table-name' = 'mysql_dest' -- MySQL table name
);

--- Query the Kafka data source table and write the computing result to the MySQL target table
INSERT INTO mysql_dest (ts,uv,pv)
SELECT TUMBLE_START(ts, INTERVAL '1' MINUTE) start_ts, COUNT(DISTINCT remote_addr) uv,count(*) pv
FROM nginx_source
GROUP BY TUMBLE(ts, INTERVAL '1' MINUTE);
```
2. On the Flink task monitoring page, view the monitoring data of the task:
![](https://qcloudimg.tencent-cloud.cn/raw/9e59652be03ac35c9e4510c2b5cc7de3.png)
3. Go to the MySQL database, and you can see that PV and UV results are calculated and written in real time:
![](https://qcloudimg.tencent-cloud.cn/raw/51cbfe4115a1130f03b24a823427b634.png)
