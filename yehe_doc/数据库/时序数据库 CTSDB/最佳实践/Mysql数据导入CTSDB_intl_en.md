
## Foreword 
CTSDB is a distributed and scalable time series database that supports near-real time data search and analysis. It is compatible with common Elasticsearch APIs. Many users may not find a good way to import MySQL data into CTSDB. Therefore, this document provides a simple and easy way to sync MySQL data into CTSDB.

## Overview 
go-mysql-elasticsearch is an open-source high-performance Elasticsearch tool developed in Go for syncing MySQL data. It is easy to compile and use, and it works in a very simple way: you first use mysqldump to get the current MySQL data, then use `name` and `position` in the current binlog to get the incremental data, and finally construct RESTful APIs based on the binlog to write the data into Elasticsearch. As CTSDB is developed based on Elasticsearch, it is perfectly compatible with go-mysql-elasticsearch for MySQL data import.

## Syncing MySQL Data to CTSDB 
### MySQL sample data construction 
As you want to import MySQL data into CTSDB, it is assumed that you have installed MySQL. To make the process complete, this document starts from the import of sample data. Here, a simple tool written in Go is used to generate some sample data and import it into MySQL with the following table structure: 
```
    mysql> desc test_table;
	+-----------+-------------+------+-----+---------+----------------+
	| Field     | Type        | Null | Key | Default | Extra          |
	+-----------+-------------+------+-----+---------+----------------+
	| id        | int(11)     | NO   | PRI | NULL    | auto_increment |
	| timestamp | bigint(20)  | YES  |     | NULL    |                |
	| cpu_usage | float       | YES  |     | NULL    |                |
	| host_ip   | varchar(20) | YES  |     | NULL    |                |
	| region    | varchar(20) | YES  |     | NULL    |                |
	+-----------+-------------+------+-----+---------+----------------+
```
Use the above code to create a table named `test_table`. Then, import 2,000 records of sample data into the table. Some data records are as shown below: 
```
    mysql> select * from test_table;
    +------+------------+-----------+-------------+-----------+
    | id   | timestamp  | cpu_usage | host_ip | region|
    +------+------------+-----------+-------------+-----------+
    |1 | 1527676339 |  0.23 | 192.168.1.1 | beijing   |
    |2 | 1527676399 |  0.78 | 192.168.1.2 | shanghai  |
    |3 | 1527676459 |   0.2 | 192.168.1.3 | guangzhou |
    |4 | 1527676519 |  0.47 | 192.168.1.4 | shanghai  |
    |5 | 1527676579 |  0.13 | 192.168.1.5 | beijing   |
    |6 | 1527676639 |  0.15 | 192.168.1.1 | beijing   |
    |7 | 1527676699 |  0.07 | 192.168.1.2 | shanghai  |
    |8 | 1527676759 |  0.17 | 192.168.1.3 | guangzhou |
    |9 | 1527676819 |  0.94 | 192.168.1.4 | shanghai  |
    |10| 1527676879 |  0.06 | 192.168.1.5 | beijing   |
```
At this point, MySQL sample data has been prepared.

### Creating metric in CTSDB 
 Create a metric in CTSDB with the same structure as that of the MySQL table by using the following API to store the corresponding data: 
```
    POST /_metric/test_metric
	{
	  "time": {
	    "name": "timestamp",   # Common time field in CTSDB, which corresponds to `timestamp` in the MySQL table
	    "format": "strict_date_optional_time || epoch_second"
	  },
	  "tags": {
	    "region": "string",
	    "host_ip": "string"
	  },
	  "fields": {
	    "cpu_usage": "float"   # The `fields` field indicates the metric column. Obviously, `cpu_usage` indicates the CPU utilization metric that needs to be monitored
	  }
	}
```
At this point, the CTSDB metric structure has been prepared. Then, use go-mysql-elasticsearch to sync data.

### go-mysql-elasticsearch usage  
As go-mysql-elasticsearch is developed in Go, you first need to install Go on a version above 1.6. Go installation is very simple. You can download it at https://golang.org/dl/ and install it as instructed in [Download and install](https://golang.org/doc/install#install). The entire process is as follows:
```
    $ go get github.com/siddontang/go-mysql-elasticsearch
	$ cd $GOPATH/src/github.com/siddontang/go-mysql-elasticsearch
	$ make
```
After the tool is installed, you need to properly configure it first before using it. The following is a configuration sample with corresponding comments:
```
   # Note: the default configuration file of go-mysql-elasticsearch is `go-mysql-elasticsearch/etc/river.toml`
	# MySQL address, user and password
	# user must have replication privilege in MySQL.
	my_addr = "127.0.0.1:3306"
	my_user = "root"
	my_pass = "123456"
	my_charset = "utf8"
	# Set true when elasticsearch use https
	#es_https = false
	# CTSDB address
	es_addr = "9.6.174.42:13982"
	# For CTSDB instances that require authentication, you need to set the username and password
	es_user = "root"
	es_pass = "changeme"
	# Path to store data, like master.info, if not set or empty,
	# we must use this to support breakpoint resume syncing. 
	# TODO: support other storage, like etcd. 
	data_dir = "./var"  # Binlog name and location
	# Inner http status address
	stat_addr = "127.0.0.1:12800"
	# pseudo server id like a slave 
	server_id = 1001
	# mysql or mariadb
	flavor = "mysql"
	# mysqldump execution path
	# if not set or empty, ignore mysqldump.
	mysqldump = "mysqldump"
	# minimal items to be inserted in one bulk
	bulk_size = 512
	# force flush the pending requests if we don't have enough items >= bulk_size
	flush_bulk_time = "200ms"
	# Ignore table without primary key
	skip_no_pk_table = true
	# MySQL data source
	[[source]]
	schema = "mysql_es"
	# Only below tables will be synced into Elasticsearch.
	# "t_[0-9]{4}" is a wildcard table format, you can use it if you have many sub tables, like table_0000 - table_1023
	# I don't think it is necessary to sync all tables in a database.
	tables = ["test_*"]
	[[rule]]
	schema = "mysql_es"   # MySQL database name
	table = "test_table"  # MySQL table name
	index = "test_metric"  # CTSDB metric name
	type = "doc"          # Document type
```
The above configuration is only for test. If you have more advanced requirements, please see the official documentation for proper configuration. After completing the configuration, run go-mysql-elasticsearch as follows: 
```
    $  ./bin/go-mysql-elasticsearch -config=./etc/river.toml
    2018/05/31 21:43:44 INFO  create BinlogSyncer with config {1001 mysql 127.0.0.1 3306 root   utf8 false false <nil> false false 0 0s 0s 0}
    2018/05/31 21:43:44 INFO  run status http server 127.0.0.1:12800
    2018/05/31 21:43:44 INFO  skip dump, use last binlog replication pos (mysql-bin.000002, 194296) or GTID %!s(<nil>)
    2018/05/31 21:43:44 INFO  begin to sync binlog from position (mysql-bin.000002, 194296)
    2018/05/31 21:43:44 INFO  register slave for master server 127.0.0.1:3306
    2018/05/31 21:43:44 INFO  start sync binlog at binlog file (mysql-bin.000002, 194296)
    2018/05/31 21:43:44 INFO  rotate to (mysql-bin.000002, 194296)
    2018/05/31 21:43:44 INFO  rotate binlog to (mysql-bin.000002, 194296)
    2018/05/31 21:43:44 INFO  save position (mysql-bin.000002, 194296)
```

Note that as go-mysql-elasticsearch needs to use binlogs in row-based format, you must configure the following parameters in MySQL: 
```
    # Configure the following parameters; otherwise, errors will definitely occur
    log_bin=mysql-bin
    binlog_format = ROW
    server-id=1
```
Now, check whether the MySQL data has been successfully imported into CTSDB: 
```
    GET test_metric/_search?size=1000
    {
      "sort": [
    {
      "timestamp": {
    "order": "desc"
      }
    }
      ], 
      "docvalue_fields": ["timestamp", "host_ip", "region", "cpu_usage"]
    }
    # Result:
    {
      "took": 8,
      "timed_out": false,
      "_shards": {
    "total": 3,
    "successful": 3,
    "skipped": 0,
    "failed": 0
      },
      "hits": {
    "total": 2000,
    "max_score": null,
    "hits": [
      {
    "_index": "test_metric@1525363200000_30",
    "_type": "doc",
    "_id": "2000",
    "_score": null,
    "fields": {
      "host_ip": [
    "192.168.1.5"
      ],
      "region": [
    "beijing"
      ],
      "cpu_usage": [
    0.05000000074505806
      ],
      "timestamp": [
    1527807286000
      ]
    },
    "sort": [
      1527807286000
    ]
      },
      ......
    }
```

## Summary 
As you can see, with go-mysql-elasticsearch, you only need to write rules in the configuration file to easily sync MySQL data to Elasticsearch. The above section only provides some simple examples. If you have more needs, please see the official documentation of go-mysql-elasticsearch.

In addition to the tool described in this document, two other tools are also recommended:
- py-mysql-elasticsearch-sync. It is written in Python, and it works in a way similar to go-mysql-elasticsearch, as both of them use binlogs to sync data. For more information on how to install and use it, please see [py-mysql-elasticsearch-sync](https://github.com/zhongbiaodev/py-mysql-elasticsearch-sync).
- Logstash. To use it to sync data, you need to install the `logstash-input-jdbc` and `logstash-output-elasticsearch` plugins. For more information on how to use it, please see [Jdbc input plugin](https://www.elastic.co/guide/en/logstash/current/plugins-inputs-jdbc.html) and [Elasticsearch output plugin](https://www.elastic.co/guide/en/logstash/current/plugins-outputs-elasticsearch.html).
If you have any questions when using the above tools, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
