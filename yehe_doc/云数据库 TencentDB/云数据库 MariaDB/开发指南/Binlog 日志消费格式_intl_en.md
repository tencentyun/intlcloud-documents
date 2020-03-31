Data subscription helps you get incremental data from TencentDB for MariaDB and TDSQL, so that you can flexibly process real-time incremental data based on your actual business needs.

## Feature List
- Data subscription is supported for TencentDB for MariaDB and TDSQL instances in public cloud.
- Data subscription is supported for TencentDB for MariaDB and TDSQL instances in private cloud.

## Data Source Type
TencentDB for MariaDB and TDSQL.

## Message Format
The data subscription feature parses instance binlogs (in row format), encapsulates binlog events into messages in JSON format, and uploads them to a Kafka cluster. Message types include `DML`, `GTID`, `XID`, and `QUERY` events, which represent modification to data rows, start of transactions, commit of transactions, and `DDL` statements, respectively. DML events include `insert`, `update`, and `delete` events.

**The message format of a `DML` event is as follows:**
```
{
    "logtype":"mysqlbinlog",          // Log type. The value is unique and must be `mysqlbinlog`
    "eventtype":23,                   // Event type code of a binlog in MySQL
  
    "eventtypestr":"insert",          / *Event type string. The value can be `insert`, `update`, `delete`, `gtid`, `xid`, or `query`.
		                                An `insert`, `update`, or `delete` event indicates `DML` statements; a `tid` event indicates start of a transaction;
                                        An `xid` event indicates end of a transaction; a `query` event indicates `DDL` statements */
    "db":"testdb",                    // Database name
    "table":"testtable",              // Table name
    "localip":"000.00.000.000",       // IP of the server where the instance is located
    "localport":0000,                 // Instance port
    "begintime":1511350073,           // Start time of the transaction to which the current event belongs
    "gtid":"0-2670193178-726233561",  // `GTID` of the transaction to which the current event belongs
    "event_index":"4",                // Number of the event in the transaction  
    "where":[                         // `where` field, which indicates the value of each field before the row is modified
    
    ],
    "field":[                         // `field` field, which indicates the value of each field after the row is modified
        "1",
        "'name1'"
    ]
}
```

**The message format of a `GTID` event is as follows:**
```
{                                    // A `GTID` event represents the start of a transaction
    "logtype":"mysqlbinlog",
    "eventtype":33,
    "eventtypestr":"gtid",
    "db":"sysdb",
    "table":"statustableforhb",
    "localip":"10.231.23.241",
    "localport":8810,
    "begintime":1511419963,
    "gtid":"35be190b-d019-11e7-ab7a-a0423f32c225:469",
    "event_index":"1"
}
```

**The message format of an `XID` event is as follows:**
```
{                                    // An `XID` event represents that a transaction has been committed
    "logtype":"mysqlbinlog",
    "eventtype":16,
    "eventtypestr":"xid",
    "db":"testsummer",
    "table":"test_table1",
    "localip":"10.231.23.241",
    "localport":8810,
    "begintime":1511419963,
    "gtid":"35be190b-d019-11e7-ab7a-a0423f32c225:469",
    "event_index":"5",
    "xid":"11866"
}
```

**The message format of a `QUERY` event is as follows:**
```
{
    "logtype":"mysqlbinlog",                          
    "eventtype":2,
    "eventtypestr":"query",         // `DDL` statement of a `QUERY` event
    "db":"testsummer",
    "table":"statustableforhb",
    "localip":"10.231.23.241",
    "localport":8810,
    "begintime":1511419941,
    "gtid":"35be190b-d019-11e7-ab7a-a0423f32c225:452",
    "event_index":"2",
    "sql":"create table test_table1 (id int primary key,name varchar(20))"
}
```


## Subscription Method
You can use message events stored in a Kafka cluster to get the data in real time and process messages after getting them through the data subscription API provided by Tencent Cloud.
