Apache Phoenix is a massively parallel relational database engine supporting OLTP for Hadoop with Apache HBase as its backing store. Phoenix compiles simple queries in just milliseconds and queries millions of rows of data in seconds. By default, the Phoenix client is integrated in HBase-enabled EMR clusters.
1. Start the client.
Switch to the `hadoop` user, go to the `/usr/local/service/hbase/phoenix-client/bin` directory, and use Phoenix's Python command line tool:
```
./sqlline.py
```
If the execution succeeds, the following result will be displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/210a079d7008c510ca25ef6c38eb8a1c.png)

2. Phoenix supports SQL queries. The following are some common operations:
  - Create a table
```sql
0: jdbc:phoenix:> CREATE TABLE IF NOT EXISTS TEST (
	host char(50) not null,
	txn_count bigint
	CONSTRAINT pk PRIMARY KEY (host)
);
```
  - Insert data
```sql
0: jdbc:phoenix:>UPSERT INTO TEST(host,txn_count) VALUES('192.168.1.1',1);
0: jdbc:phoenix:>UPSERT INTO TEST(host,txn_count) VALUES('192.168.1.2',2);
```
  - Query data
```sql
0: jdbc:phoenix:>SELECT * FROM TEST;
```
  - Delete a data table
```sql
0: jdbc:phoenix:>DROP TABLE IF EXISTS TEST;
```

For more operations and instructions, see [Grammar](http://phoenix.apache.org/language/index.html).
