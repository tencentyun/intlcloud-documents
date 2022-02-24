This document describes how to import data from a local file to Cloud Data Warehouse.

## Prerequisites
1. The ClickHouse client has been installed. If not, you can [download](https://repo.yandex.ru/clickhouse/rpm/stable/x86_64/) and install it.
2. The following common file formats can be imported to Cloud Data Warehouse: TabSeparated, TabSeparatedRaw, TabSeparatedWithNames, TabSeparatedWithNamesAndTypes, Template, CSV, and CSVWithNames. For more supported formats, see [Formats for Input and Output Data](https://clickhouse.com/docs/zh/interfaces/formats/#tabseparated).
3. Make sure that the local server where the ClickHouse client is installed and the Cloud Data Warehouse cluster are in the same VPC.

>!
- Client and server versions are compatible, but some features may not be available on earlier clients. We recommend you use a client of the same version as the server. When you use a legacy client, the client on the server will display the following message: "ClickHouse client version is older than ClickHouse server. It may lack support for new features." In this case, import a file using the following command: `cat <data_file> | ./clickhouse-client --host=<host> --port=<port> --user=<username> --password=<password> --query="INSERT INTO <table_name> FORMAT <format>";`
- In batch mode, the default data format is TabSeparated. You can set a format flexibly based on the query.
By default, the batch mode supports only a single query. In order to execute multiple queries from a single script, use the `--multiquery` parameter, which is useful in most cases except for INSERT requests. The query results are output continuously without delimiters. Similarly, to execute large-scale queries, start a ClickHouse client for each query. Note that each startup takes tens of milliseconds.

## Directions
The following is the entire process of importing the local file `test.csv`.
1. Prepare `test.csv` and write the following data.
```
$ cat /test.csv
    1,2,3
    3,2,1
    78,43,45
```
2. Create a ClickHouse target table.
    - If your cluster has one replica:
```
CREATE TABLE test.test on cluster default_cluster
(
    `column1` UInt32,
    `column2` UInt32,
    `column3` UInt32
)
engine = MergeTree()
order by column1;
```
    - If your cluster has two replicas:
```
create table test.test on cluster default_cluster
(
    `column1` UInt32,
    `column2` UInt32,
    `column3` UInt32
)
engine = ReplicatedMergeTree('/clickhouse/tables/test/test/{shard}', '{replica}')
order by column1;
```
    - Create a distributed table:
```
create table test.test_dis on cluster default
AS test.test
engine = Distributed('default_cluster', 'test', 'test', rand());
```


3. Write data to the target table.
```
cat data.csv | clickhouse-client --query="INSERT INTO test FORMAT CSV"
```

4. Query the data.
```
select * from test;
```
