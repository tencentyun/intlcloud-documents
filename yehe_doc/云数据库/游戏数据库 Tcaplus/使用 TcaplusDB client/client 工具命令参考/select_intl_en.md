## Overview
This command is used to query the entire record or several fields included in the record. If no record is matched, an error will be returned.

## Syntax
```
select key1, key2, key3, value1, value2 [into result.csv] from table where key1 = 1 and key2 = "abc" [and -index = 1] [\P] [\G] [using tdr]
select * [into result.xml] from table where key1 = 1 and key2 = "abc" [and -index = 1] using tdr [\P];
```

## Parameters

|  Parameter          | Protobuf                                      | TDR                             | Required       |
| --------- | ---------------------------------------- | -------------------------------------------- | ------------ |
| table     | Table name                                                  | Table name                             | Yes           |
| key       | Primary key field name. The global index query is supported. You can enter some key values.      | Primary key field name. All key values are required.        | Yes     |
| value     | Non-primary key field name                  | Non-primary key field name                                 | Yes, at least one |
| \-index   | LIST table: if `\-index` is specified, the index record under the same key will be returned; if `\-index` is not specified, all records will be returned.<br>GENERIC table: not supported | LIST table: if `\-index` is specified, the index record under the same key will be returned; if `\-index` is not specified, all records will be returned.<br>GENERIC table: not supported | No           |
| \\P       | Printing latency                              | Printing latency                           | No           |
| \\G       | Vertical printing                                   | Vertical printing                                    | No           |
| using tdr | Not supported                 | When data is output in XML format, the file structure must strictly comply with the XML syntax. A TDR file must be provided when the client is started. | No           |
| into      | Output data to the file                           | Output data to the file                           | No           |


## Errors
For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1016/38791).

## Sample

```
tcaplus> select * from test_table where gameid=1234 and itemid=12323 and name='testname';
+------+------+----------+------+----+-----+
|gameid|itemid|name      |typeid|Data|uname|
+------+------+----------+------+----+-----+
|1234  |12323 |"testname"|0     |9   |"ab" |
+------+------+----------+------+----+-----+
1 records selectd, select time: 9802 us
 
tcaplus> select uname from test_table where gameid=1234 and itemid=12323 and name='testname';
+------+------+----------+-----+
|gameid|itemid|name      |uname|
+------+------+----------+-----+
|1234  |12323 |"testname"|"ab" |
+------+------+----------+-----+
1 records selectd, select time: 9457 us
 
tcaplus> select * into test.txt from test_table where gameid=1234 and itemid=12323 and name='testname';
1 records are stored to test.csv, select time: 10198 us
 
tcaplus> select * from test_table where gameid=1234 and itemid=12323 and name='testname' \P \G;
gameid: 1234
itemid: 12323
name: "testname"
typeid: 0
Data: 9
uname: "ab"
 
API ----      -1us    --->ProxyFront----      10us    --->ProxyEnd---     364us    --->SvrMainStart
|                              |                             |                           |381us
|11380us                       |4138us                       |4104us                   SvrWorkerStart
|                              |                             |                           |61us
API <---   34197us    ----ProxyFront<---      24us    ----ProxyEnd<--    3298us    ----SvrWorkerEnd
1 records selectd, select time: 11380 us
 
 
tcaplus> select * into table_list.xml from table_list where uin=99 and name = "99" and key1=99 using tdr;
11 records are stored to table_list.xml, select time: 135299 us
 
tcaplus> select c_string from table_list where uin=99 and name = "99" and key1=99;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |""      |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
11 records selectd, select time: 102572 us
 
tcaplus> select c_string from table_list where uin=99 and name = "99" and key1=99 and -index=9;
+---+----+----+--------+
|uin|name|key1|c_string|
+---+----+----+--------+
|99 |"99"|99  |" "     |
+---+----+----+--------+
1 records selectd, select time: 9886 us
```

