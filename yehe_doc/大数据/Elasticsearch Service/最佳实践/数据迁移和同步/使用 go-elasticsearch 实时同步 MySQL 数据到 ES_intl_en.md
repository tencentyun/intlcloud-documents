This document describes how to sync data in MySQL to ES in real time by syncing the MySQL binlog, which can implement low-latency data search and analysis. This method has been proven feasible and is illustrated for your reference.

## MySQL Binlog
MySQL's binlog is mainly used for source-replica replication and data recovery in databases. The binlog records the CRUD operations performed on the data. During the source-replica replication process, the source database syncs its binlog to the replica database which replays the events stored in the binlog to achieve source-replica sync.

MySQL binlog has three logging modes, namely:
- ROW: It records the changes to each data row, which, however, generates a high number of logs.
- STATEMENT: It records each executed SQL statement that modifies the data, which reduces the number of logs; however, source-replica inconsistency often occurs when SQL statements use functions or triggers.
- MIXED: It combines the advantages of ROW and STATEMENT by choosing either ROW or STATEMENT to generate logs based on the specific SQL statement that performs data operations.

To sync data to an ES cluster with MySQL binlog, you can only use ROW mode, because only this mode knows what is modified in the MySQL data. The following shows the binlog contents in ROW and STATEMENT modes with an UPDATE operation as an example.
- The binlog contents in ROW mode are as follows:
```
SET TIMESTAMP=1527917394/*!*/;
BEGIN
/*!*/;
# at 3751
#180602 13:29:54 server id 1  end_log_pos 3819 CRC32 0x8dabdf01 	Table_map: `webservice`.`building` mapped to number 74
# at 3819
#180602 13:29:54 server id 1  end_log_pos 3949 CRC32 0x59a8ed85 	Update_rows: table id 74 flags: STMT_END_F
BINLOG '
UisSWxMBAAAARAAAAOsOAAAAAEoAAAAAAAEACndlYnNlcnZpY2UACGJ1aWxkaW5nAAYIDwEPEREG
wACAAQAAAAHfq40=
UisSWx8BAAAAggAAAG0PAAAAAEoAAAAAAAEAAgAG///A1gcAAAAAAAALYnVpbGRpbmctMTAADwB3
UkRNbjNLYlV5d1k3ajVbD64WWw+uFsDWBwAAAAAAAAtidWlsZGluZy0xMAEPAHdSRE1uM0tiVXl3
WTdqNVsPrhZbD64Whe2oWQ==
'/*!*/;
### UPDATE `webservice`.`building`
### WHERE
###   @1=2006 /* LONGINT meta=0 nullable=0 is_null=0 */
###   @2='building-10' /* VARSTRING(192) meta=192 nullable=0 is_null=0 */
###   @3=0 /* TINYINT meta=0 nullable=0 is_null=0 */
###   @4='wRDMn3KbUywY7j5' /* VARSTRING(384) meta=384 nullable=0 is_null=0 */
###   @5=1527754262 /* TIMESTAMP(0) meta=0 nullable=0 is_null=0 */
###   @6=1527754262 /* TIMESTAMP(0) meta=0 nullable=0 is_null=0 */
### SET
###   @1=2006 /* LONGINT meta=0 nullable=0 is_null=0 */
###   @2='building-10' /* VARSTRING(192) meta=192 nullable=0 is_null=0 */
###   @3=1 /* TINYINT meta=0 nullable=0 is_null=0 */
###   @4='wRDMn3KbUywY7j5' /* VARSTRING(384) meta=384 nullable=0 is_null=0 */
###   @5=1527754262 /* TIMESTAMP(0) meta=0 nullable=0 is_null=0 */
###   @6=1527754262 /* TIMESTAMP(0) meta=0 nullable=0 is_null=0 */
# at 3949
#180602 13:29:54 server id 1  end_log_pos 3980 CRC32 0x58226b8f 	Xid = 182
COMMIT/*!*/;
```
- The binlog contents in STATEMENT mode are as follows:
```
SET TIMESTAMP=1527919329/*!*/;
update building set Status=1 where Id=2000
/*!*/;
# at 688
#180602 14:02:09 server id 1  end_log_pos 719 CRC32 0x4c550a7d 	Xid = 200
COMMIT/*!*/;
```

As can be seen from the log contents of the UPDATE operation in ROW and STATEMENT modes, the ROW mode completely records the values of all fields in the row to be modified before and after the update, while the STATEMENT mode only records the SQL statement of the UPDATE operation. Therefore, if you need to sync MySQL data to ES in real time, you can only choose the binlog in ROW mode, obtain and parse the data contents in the binlog, and execute the ES document API to sync the data to the ES cluster.

## mysqldump Tool
`mysqldump` is a tool for exporting full data from a MySQL database. It can be used in the following way:
```
mysqldump -uelastic -p'Elastic_123' --host=172.16.32.5 -F webservice > dump.sql
```
The above command indicates to export all data of `database:webservice` from the remote database `172.16.32.5:3306` and write to the `dump.sql` file. The `-F` parameter indicates to generate a new binlog file after exporting the data to log all subsequent data operations. The contents of the `dump.sql` file are as follows:
```
-- MySQL dump 10.13  Distrib 5.6.40, for Linux (x86_64)
--
-- Host: 172.16.32.5    Database: webservice
-- ------------------------------------------------------
-- Server version	5.5.5-10.1.9-MariaDBV1.0R012D002-20171127-1822

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `building`
--

DROP TABLE IF EXISTS `building`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!40101 SET character_set_client = utf8 */;
CREATE TABLE `building` (
  `Id` bigint(20) unsigned NOT NULL AUTO_INCREMENT COMMENT 'ID',
  `BuildingId` varchar(64) NOT NULL COMMENT 'Virtual building ID',
  `Status` tinyint(4) NOT NULL DEFAULT '0' COMMENT 'Virtual building status. 0: processing; 1: normal; -1: stopped; -2: terminating; -3: terminated',
  `BuildingName` varchar(128) NOT NULL DEFAULT '' COMMENT 'Virtual building name',
  `CreateTime` timestamp NOT NULL DEFAULT '2017-12-03 16:00:00' COMMENT 'Creation time',
  `UpdateTime` timestamp NOT NULL DEFAULT '2017-12-03 16:00:00' COMMENT 'Update time',
  PRIMARY KEY (`Id`),
  UNIQUE KEY `BuildingId` (`BuildingId`)
) ENGINE=InnoDB AUTO_INCREMENT=2010 DEFAULT CHARSET=utf8 COMMENT='Virtual building table';
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `building`
--

LOCK TABLES `building` WRITE;
/*!40000 ALTER TABLE `building` DISABLE KEYS */;
INSERT INTO `building` VALUES (2000,'building-2',0,'6YFcmntKrNBIeTA','2018-05-30 13:28:31','2018-05-30 13:28:31'),(2001,'building-4',0,'4rY8PcVUZB1vtrL','2018-05-30 13:28:34','2018-05-30 13:28:34'),(2002,'building-5',0,'uyjHVUYrg9KeGqi','2018-05-30 13:28:37','2018-05-30 13:28:37'),(2003,'building-7',0,'DNhyEBO4XEkXpgW','2018-05-30 13:28:40','2018-05-30 13:28:40'),(2004,'building-1',0,'TmtYX6ZC0RNB4Re','2018-05-30 13:28:43','2018-05-30 13:28:43'),(2005,'building-6',0,'t8YQcjeXefWpcyU','2018-05-30 13:28:49','2018-05-30 13:28:49'),(2006,'building-10',0,'WozgBc2IchNyKyE','2018-05-30 13:28:55','2018-05-30 13:28:55'),(2007,'building-3',0,'yJk27cmLOVQLHf1','2018-05-30 13:28:58','2018-05-30 13:28:58'),(2008,'building-9',0,'RSbjotAh8tymfxs','2018-05-30 13:29:04','2018-05-30 13:29:04'),(2009,'building-8',0,'IBOMlhaXV6k226m','2018-05-30 13:29:31','2018-05-30 13:29:31');
/*!40000 ALTER TABLE `building` ENABLE KEYS */;
UNLOCK TABLES;

/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2018-06-02 14:23:51
```
As can be seen from the above, the SQL file exported by mysqldump contains SQL statements for creating table, dropping table, and inserting data, but does not contain the statement for creating database.

## Using Open-Source go-mysql-elasticsearch Tool to Sync Data to ES
`go-mysql-elasticsearch` is an open-source tool for syncing MySQL data to an ES cluster. For more information, see its [GitHub page](https://github.com/siddontang/go-mysql-elasticsearch).

The following describes how `go-mysql-elasticsearch` works. When you launch it for the first time, use the `mysqldump` tool to perform a full sync of the source MySQL database first and write the data to ES through the Elasticsearch client; then, implement a MySQL client as the replica, connect it to the source MySQL database which, as the source, will sync all data updates to the replica through binlog events. By parsing such events, the updated contents of the data can be obtained and written to ES.

In addition, this tool also provides the feature to count operations. When a data addition, deletion, or update is performed, the count of the corresponding operation will be increased by 1. When the program starts, an HTTP service will be launched, and the number of additions, deletions, and updates can be viewed by calling the HTTP API.

### Use limits
1. MySQL binlog must use ROW mode (which is enabled in TencentDB for MySQL by default).
2. The MySQL data table to be synced must contain a primary key; otherwise, it will be ignored directly. If the data table has no primary key, the UPDATE and DELETE operations cannot find the corresponding documents in ES, causing a sync failure.
3. Table structure cannot be modified when the program is running.
4. You need to grant the account used to connect to MySQL the RELOAD, REPLICATION, and VIEW permissions; otherwise, the program will exit abnormally when you create an account in the database.
```
GRANT REPLICATION SLAVE ON *.* TO 'elastic'@'172.16.32.44';
GRANT RELOAD ON *.* TO 'elastic'@'172.16.32.44';
```

### How to use
1. Install Go 1.10+. You can simply install the latest version of Go and then set the `GOPATH` environment variable.
2. Run the `go get github.com/siddontang/go-mysql-elasticsearch` command.
3. Run the `cd $GOPATH/src/github.com/siddontang/go-mysql-elasticsearch` command.
4. Run the `make` command to start compiling. After the compilation is successful, an executable file named `go-mysql-elasticsearch` will be generated in the `go-mysql-elasticsearch/bin` directory.
5. Run the `vi etc/river.toml` command to modify the configuration file so as to sync the `webservice.building` table in the `172.16.0.101:3306` database to the building index of the `172.16.32.64:9200` ES cluster. (For detailed description of the configuration file, see the [project documentation](https://github.com/siddontang/go-mysql-elasticsearch).)	
```
	# MySQL address, user and password
	# user must have replication privilege in MySQL.
	my_addr = "172.16.0.101:3306"
	my_user = "bellen"
	my_pass = "Elastic_123"
	my_charset = "utf8"
	
	# Set true when elasticsearch use https
	#es_https = false
	# Elasticsearch address
	es_addr = "172.16.32.64:9200"
	# Elasticsearch user and password, maybe set by shield, nginx, or x-pack
	es_user = ""
	es_pass = ""
	
	# Path to store data, like master.info, if not set or empty,
	# we must use this to support breakpoint resume syncing.
	# TODO: support other storage, like etcd.
	data_dir = "./var"
	
	# Inner Http status address
	stat_addr = "127.0.0.1:12800"
	
	# pseudo server id like a slave
	server_id = 1001
	
	# mysql or mariadb
	flavor = "mariadb"
	
	# mysqldump execution path
	# if not set or empty, ignore mysqldump.
	mysqldump = "mysqldump"
	
	# if we have no privilege to use mysqldump with --master-data,
	# we must skip it.
	#skip_master_data = false
	
	# minimal items to be inserted in one bulk
	bulk_size = 128
	
	# force flush the pending requests if we don't have enough items >= bulk_size
	flush_bulk_time = "200ms"
	
	# Ignore table without primary key
	skip_no_pk_table = false
	
	# MySQL data source
	[[source]]
	schema = "webservice"
	tables = ["building"]
	[[rule]]
	schema = "webservice"
	table = "building"
	index = "building"
	type = "buildingtype"
```
6. Create a building index in the ES cluster, because the tool does not use the "auto create index" feature of ES, and an error will be displayed if the index does not exist.
7. Run the `./bin/go-mysql-elasticsearch -config=./etc/river.toml` command.
8. Output the result in the console.
```
	2018/06/02 16:13:21 INFO  create BinlogSyncer with config {1001 mariadb 172.16.0.101 3306 bellen   utf8 false false <nil> false false 0 0s 0s 0}
	2018/06/02 16:13:21 INFO  run status http server 127.0.0.1:12800
	2018/06/02 16:13:21 INFO  skip dump, use last binlog replication pos (mysql-bin.000001, 120) or GTID %!s(<nil>)
	2018/06/02 16:13:21 INFO  begin to sync binlog from position (mysql-bin.000001, 120)
	2018/06/02 16:13:21 INFO  register slave for master server 172.16.0.101:3306
	2018/06/02 16:13:21 INFO  start sync binlog at binlog file (mysql-bin.000001, 120)
	2018/06/02 16:13:21 INFO  rotate to (mysql-bin.000001, 120)
	2018/06/02 16:13:21 INFO  rotate binlog to (mysql-bin.000001, 120)
	2018/06/02 16:13:21 INFO  save position (mysql-bin.000001, 120)
```
9. Test: Data insertion, update, and deletion performed in MySQL can be reflected in ES.
10. ES 7.x only allows table names that contain (_doc). When the program inserts data, the `type` field controls the table name. Earlier versions are not affected, while new versions only allow `_doc`, so the `type` field can only be `_doc`.
```
[[rule]]
schema = "rule1"
table = "table1"
index = "table1"
type = '_doc'
[[rule]]
schema = "rule2"
table = "table2"
index = "table2"
type = "_doc"
```

### User experience
- `go-mysql-elasticsearch` provides the most basic capability to sync data from MySQL to ES in real time. If your business requires more complex features such as modifying the MySQL table structure during operation, you can customize it for secondary development.
- The tool is not good at handling exceptions. If parsing binlog events fails, it will throw an exception directly.
- As described by the tool developer, the tool has not been applied to a production environment, so we recommend you read the source code carefully to understand its pros and cons.

## Syncing Data to ES Cluster with mypipe
mypipe is a MySQL binlog sync tool initially designed to send binlog events to Kafka. It can also sync data to any storage media based on your actual business needs. For more information, see its [GitHub page](https://github.com/mardambey/mypipe).

### Use limits
1. MySQL binlog must use ROW mode.
2. You need to grant the account used to connect to MySQL the REPLICATION permission.
```
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'elastic'@'%' IDENTIFIED BY 'Elastic_123'
```
3. mypipe just parses the contents of the binlog, encodes them into Avro format, and pushes them to a Kafka broker instead of directly pushing data to Kafka. If you need to sync data to an ES cluster, you can consume the data from Kafka first and then write it to ES.
4. To consume messages in Kafka (operations log of MySQL), you need to perform Avro parsing on the message contents and obtain the corresponding data operations for further processing. mypipe encapsulates a `KafkaGenericMutationAvroConsumer` class that can be directly inherited for use. You can also implement the parsing on your own.
5. mypipe supports syncing only binlog but not existing data, i.e., after the mypipe program is started, existing data in MySQL cannot be synced.
		
### How to use
1. Run the `git clone https://github.com/mardambey/mypipe.git` command.
2. Run the `./sbt package` command.
3. Configure `mypipe-runner/src/main/resources/application.conf`.
```
	mypipe {
	
	  # Avro schema repository client class name
	  schema-repo-client = "mypipe.avro.schema.SchemaRepo"
	
	  # consumers represent sources for mysql binary logs
	  consumers {
	
	    localhost {
	      # database "host:port:user:pass" array
	      source = "172.16.0.101:3306:elastic:Elastic_123"
	    }
	  }
	
	  # data producers export data out (stdout, other stores, external services, etc.)
	  producers {
	
	    kafka-generic {
	      class = "mypipe.kafka.producer.KafkaMutationGenericAvroProducer"
	    }
	  }
	
	  # pipes join consumers and producers
	  pipes {
	
	    kafka-generic {
	      enabled = true
	      consumers = ["localhost"]
	      producer {
	        kafka-generic {
	          metadata-brokers = "172.16.16.22:9092"
	        }
	      }
	      binlog-position-repo {
	        # saved to a file, this is the default if unspecified
	        class = "mypipe.api.repo.ConfigurableFileBasedBinaryLogPositionRepository"
	        config {
	          file-prefix = "stdout-00"     # required if binlog-position-repo is specifiec
	          data-dir = "/tmp/mypipe/data" # defaults to mypipe.data-dir if not present
	        }
	      }
	    }
	  }
	}
``` 
4. Configure `mypipe-api/src/main/resources/reference.conf` by modifying the `include-event-condition` option to specify the database and table to be synced.
```
include-event-condition = """ db == "webservice" && table =="building" """
```
5. Create `topic: webservice_building_generic` on the Kafka broker. By default, mypipe uses `${db}_${table}_generic` as the topic name to send data to the topic.
6. Run the `./sbt "project runner" "runMain mypipe.runner.PipeRunner"` command.
7. Test: Insert data into the MySQL building table and write a simple consumer to consume the messages pushed to Kafka by mypipe.
8. The consumed data that has not been parsed yet is as follows:
```
ConsumerRecord(topic=u'webservice_building_generic', partition=0, offset=2, timestamp=None, timestamp_type=None, key=None, value='\x00\x01\x00\x00\x14webservice\x10building\xcc\x01\x02\x91,\xae\xa3fc\x11\xe8\xa1\xaaRT\x00Z\xf9\xab\x00\x00\x04\x18BuildingName\x06xxx\x14BuildingId\nId-10\x00\x02\x04Id\xd4%\x00', checksum=128384379, serialized_key_size=-1, serialized_value_size=88)
```

### User experience
- mypipe is more sophisticated than go-mysql-elasticsearch. It supports performing ALTER TABLE operations during running and configuring different policies to handle exceptions of binlog parsing.
- mypipe cannot sync existing data. If you need this feature, you can use other means to sync full data and then use mypipe for incremental sync.
- mypipe only syncs binlog. If you need to sync data to ES, separate development will be required.
