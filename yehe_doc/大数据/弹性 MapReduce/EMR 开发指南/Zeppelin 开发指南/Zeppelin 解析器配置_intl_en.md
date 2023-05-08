This document describes how to configure and verify common interpreters for Zeppelin (v0.91 or later is used as an example).
## Spark Interpreter
#### Configuration
```
SPARK_HOME: /usr/local/service/spark
spark.master: yarn
spark.submit.deployMode: cluster
spark.app.name: zeppelin-spark
```
#### Verification
1. Upload the `wordcount.txt` file to the `/tmp` path of `emr hdfs` first.
2. Find the `hdfs://HDFS45983` value of the `fs.defaultFS` configuration item in `core-site.xml`.
3. Run the Spark code in the notebook.
```
%spark
val data = sc.textFile("hdfs://HDFS45983/tmp/wordcount.txt")
case class WordCount(word: String, count: Integer)
val result = data.flatMap(x => x.split(" ")).map(x => (x, 1)).reduceByKey(_ + _).map(x => WordCount(x._1, x._2))
result.toDF().registerTempTable("result")

%sql 
select * from result
```

## Flink Interpreter
#### Configuration
```
FLINK_HOME: /usr/local/service/flink

flink.execution.mode: yarn
```
#### Verification
```
%flink
val data = benv.fromElements("hello world", "hello flink", "hello hadoop")
data.flatMap(line => line.split("\\s"))
             .map(w => (w, 1))
             .groupBy(0)
             .sum(1)
             .print()
```

## HBase Interpreter
#### Configuration
```
hbase.home: /usr/local/service/hbase

hbase.ruby.sources: lib/ruby

zeppelin.hbase.test.mode: false
```
>! As the JAR packages depended on by this interpreter have been integrated into the `/usr/local/service/zeppelin/local-repo` path of the cluster, you don't need to configure dependencies. They are required only if you want to define JAR packages.

#### Verification
```
%hbase
help 'get'

%hbase
list
```

## Livy Interpreter
#### Configuration
```
zeppelin.livy.url: http://ip:8998
```
#### Verification
```
%livy.spark
sc.version

%livy.pyspark
print "1"

%livy.sparkr
hello <- function( name ) {
    sprintf( "Hello, %s", name );
}
hello("livy")
```

## Kylin Interpreter
#### Configuration
1. Create a default project in the Kylin console.
2. Configure the Kylin interpreter for Zeppelin.
```
kylin.api.url: http://ip:16500/kylin/api/query

kylin.api.user: ADMIN

kylin.api.password: KYLIN

kylin.query.project: default
```
#### Verification
```
%kylin(default)

select count(*) from table1
```

## JDBC Interpreters
### 1. MySQL interpreter configuration
```
default.url: jdbc:mysql://ip:3306

default.user: xxx

default.password: xxx

default.driver: com.mysql.jdbc.Driver
```
>! As the JAR packages depended on by this interpreter have been integrated into the `/usr/local/service/zeppelin/local-repo` path of the cluster, you don't need to configure dependencies. They are required only if you want to define JAR packages.
>
#### Verification
```
%mysql
show databases

```

### 2. Hive interpreter configuration
```
default.url: jdbc:hive2://ip:7001

default.user: hadoop

default.password: 

default.driver: org.apache.hive.jdbc.HiveDriver
```
>! As the JAR packages depended on by this interpreter have been integrated into the `/usr/local/service/zeppelin/local-repo` path of the cluster, you don't need to configure dependencies. They are required only if you want to define JAR packages.
>
#### Verification
```
%hive
show databases

%hive
use default;
show tables;
```

### 3. Presto interpreter configuration
```
default.url: jdbc:presto://ip:9000?user=hadoop

default.user: hadoop

default.password:

default.driver: io.prestosql.jdbc.PrestoDriver
```
>! As the JAR packages depended on by this interpreter have been integrated into the `/usr/local/service/zeppelin/local-repo` path of the cluster, you don't need to configure dependencies. They are required only if you want to define JAR packages.
>
#### Verification
```
%presto
show catalogs;

%presto
show schemas from hive;

%presto
show tables from hive.default;
```

For more versions and interpreter configuration, see [Zeppelin Documentation](https://zeppelin.apache.org/docs/0.9.0/interpreter/jdbc.html).
