## Overview
This document describes two methods to import HDFS data to a ClickHouse cluster suitable for scenarios with low and high data volumes respectively. **In this document, v19.16.12.49 is used as an example.**

>?To share your thoughts on ClickHouse, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to join the ClickHouse technical exchange group.

## Directions

### Importing data from external table

This method is suitable for scenarios where the data volume is small and can be implemented in the following steps:
- Create an HDFS engine external table in ClickHouse to read the HDFS data.
- Create a regular table (generally in the `MergeTree` family) in ClickHouse to store the HDFS data.
- Select data from the external table (with the `SELECT` statement) and insert it into the regular table (with the `INSERT` statement) to import the data.

#### **Step 1. Create an HDFS engine external table**
```
CREATE TABLE source
(
    `id` UInt32, 
    `name` String, 
    `comment` String
)
ENGINE = HDFS('hdfs://172.30.1.146:4007/clickhouse/globs/*.csv', 'CSV')
```

For more information on how to use the HDFS engine (`ENGINE = HDFS(URI, format)`), please see [HDFS](https://clickhouse.tech/docs/en/operations/table_engines/hdfs/).

`URI` is the HDFS path. If it contains wildcards, the table is read-only. File match with wildcards is performed during the query rather than during table creation. Therefore, if the number or content of matched files changes between two queries, the difference will be shown in the query results. Supported wildcards are as follows:
- `*` can match a random number of any characters except the path separator `/`, including an empty string.
- `?` can match a character.
- `{some_string,another_string,yet_another_one}` can match `some_string`, `another_string`, or `yet_another_one`.
- `{N..M}` can match numbers from `N` to `M` (including `N` and `M`); for example, `{1..3}` can match 1, 2, and 3.


 For more information on the formats supported for `format`, please see [Formats for Input and Output Data](https://clickhouse.tech/docs/en/interfaces/formats/#formats).



#### **Step 2. Create a regular table**
```
CREATE TABLE dest
(
    `id` UInt32, 
    `name` String, 
    `comment` String
)
ENGINE = MergeTree()
ORDER BY id
```

#### Step 3. Import data
```
INSERT INTO dest SELECT *
FROM source
```

#### Step 4. Query data
```
SELECT *
FROM dest
LIMIT 2
```

### Concurrent JDBC driver import scheme
ClickHouse provides methods to access JDBC and an official driver. You can also use third-party drivers. For more information, please see [JDBC Driver](https://clickhouse.tech/docs/en/interfaces/jdbc/).

ClickHouse is deeply integrated with big data ecosystems such as Hadoop and Spark. By developing Spark or MapReduce applications and leveraging the concurrent processing capabilities of the big data platform, you can quickly import a high volume of data from HDFS to ClickHouse. Spark also supports other data sources such as Hive; therefore, you can import data from other data sources in a similar way.

**The following uses Spark Python as an example to describe how to import data concurrently:**

#### Step 1. Create a regular table

```
CREATE TABLE default.hdfs_loader_table
(
    `id` UInt32, 
    `name` String, 
    `comment` String
)
ENGINE = MergeTree()
PARTITION BY id
ORDER BY id
```

#### Step 2. Develop a Spark Python application

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
 
from pyspark.sql import SparkSession
import sys
 
if __name__ == '__main__':
    if len(sys.argv) != 2:
        print("Usage: clickhouse-spark <path>", file=sys.stderr)
        sys.exit(-1)
 
    spark = SparkSession.builder \
        .appName("clickhouse-spark") \
        .enableHiveSupport() \
        .getOrCreate()
 
    url = "jdbc:clickhouse://172.30.1.15:8123/default"
    driver = 'ru.yandex.clickhouse.ClickHouseDriver'
    properties = {
        'driver': driver,
        "socket_timeout": "300000",
        "rewriteBatchedStatements": "true",
        "batchsize": "1000000",
        "numPartitions": "4",
        'user': 'default',
        'password': 'test'
    }
    spark.read.csv(sys.argv[1], schema="""id INT, name String, comment String""").write.jdbc(
        url=url,
        table='hdfs_loader_table',
        mode='append',
        properties=properties,
    )
```

The URL format is `jdbc:clickhouse://host:port/database` where `port` is the HTTP protocol port of ClickHouse, which is 8123 by default.

The meanings of some parameters in `properties` are as follows:
- `socket_timeout` is the timeout period in milliseconds. For more information, please see [here](https://github.com/ClickHouse/clickhouse-jdbc/issues/159#issuecomment-364423414).
- `rewriteBatchedStatements` is used to enable batch SQL execution in the JDBC driver.
- `batchsize` specifies the number of data entries that can be written at a time. You can increase the value appropriately to improve the write performance.
- `numPartitions` specifies the data write concurrency, which also determines the number of JDBC concurrent connections. For more information on `batchsize` and `numPartitions`, please see [JDBC to Other Databases](https://spark.apache.org/docs/latest/sql-data-sources-jdbc.html).


#### Step 3. Submit a Spark task

```
#!/usr/bin/env bash
 
spark-submit \
  --master yarn \
  --jars ./clickhouse-jdbc-0.2.4.jar,./guava-19.0.jar \
  clickhouse-spark.py hdfs:///clickhouse/globs
```

For Spark Python, you need to check the JAR version depended on by `clickhouse-jdbc-0.2.4.jar`. You can decompress the JAR file and view the configuration in `pom.xml` to check whether the JAR package for the Spark environment matches the version; and if not, the error "[Could not initialize class ru.yandex.clickhouse.ClickHouseUtil](https://github.com/ClickHouse/clickhouse-jdbc/issues/138)" may occur. In this case, you need to download the JAR package on the correct version and submit it with the parameter `--jars` in the `spark-submit` command.

#### Step 4. Query data

```
SELECT *
FROM hdfs_loader_table
LIMIT 2
```

## Notes

This section describes two ways to directly read/write HDFS data, which are generally used to import data from HDFS to ClickHouse. They are relatively slow in read/write and do not support the following features (for more information, please see [HDFS](https://clickhouse.tech/docs/en/operations/table_engines/hdfs/)):
- `ALTER` and `SELECT...SAMPLE` operations
- Indexes
- Replication

### Table engine

1. Create a table
```
CREATE TABLE hdfs_engine_table(id UInt32, name String, comment String) ENGINE=HDFS('hdfs://172.30.1.146:4007/clickhouse/hdfs_engine_table', 'CSV')
```
1. Insert the testing data
```
INSERT INTO hdfs_engine_table VALUES(1, 'zhangsan', 'hello zhangsan'),(2, 'lisi', 'hello lisi')
```
1. Query the data
```
SELECT * FROM hdfs_engine_table
┌─id─┬─name─────┬─comment────────┐
│  1 │ zhangsan │ hello zhangsan │
│  2 │ lisi     │ hello lisi     │
└────┴──────────┴────────────────┘
```
1. View the HDFS file
```
hadoop fs -cat /clickhouse/hdfs_engine_table
1,"zhangsan","hello zhangsan"
2,"lisi","hello lisi"
```

### Table function

There is only a slight difference in the table creation syntax between using a table function and using a table engine. The sample code is as follows:
```
CREATE TABLE hdfs_function_table AS hdfs('hdfs://172.30.1.146:4007/clickhouse/hdfs_function_table', 'CSV', 'id UInt32, name String, comment String')
```


## References

- [ClickHouse Documentation - Table Engine HDFS](https://clickhouse.tech/docs/en/operations/table_engines/hdfs/)
- [ClickHouse Documentation - Table Function hdfs](https://clickhouse.tech/docs/en/query_language/table_functions/hdfs/)
- [How to Import Data from HDFS to ClickHouse?](https://blog.csdn.net/yangzhaohui168/article/details/88583489)
- [How to import my data from HDFS?](https://github.com/ClickHouse/ClickHouse/issues/1614)
- [ClickHouse Documentation - JDBC Driver](https://clickhouse.tech/docs/en/interfaces/jdbc/)
- [Summary for Writing Data to ClickHouse from Spark JDBC](https://toutiao.io/posts/m63yw89/preview)
