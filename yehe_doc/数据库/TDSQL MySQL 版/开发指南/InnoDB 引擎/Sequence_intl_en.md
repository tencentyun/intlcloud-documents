The sequence keyword syntax is compatible with MariaDB/Oracle, but a sequence must be globally incremental and unique. The specific usage is as follows:

>?
>- When using a sequence in TDSQL for MySQL, the keyword must be prefixed with `tdsql_`, and the proxy version must be later than 1.19.5-M-V2.0R745D005. You can view the proxy version by running the `/*Proxy*/show status` statement. If the proxy is on an earlier version, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for upgrade.
>- Currently, sequence is used to guarantee the global uniqueness of the distributed transaction, which has a relatively low performance and is therefore only suitable for scenarios with low concurrency.

Creating a sequence requires the `CREATE SEQUENCE` system permission. The creation syntax is as follows:
```
　　CREATE TDSQL_SEQUENCE sequence name
　　[START WITH n]
　　[{TDSQL_MINALUE/ TDSQL_MAXMINVALUE n| TDSQL_NOMAXVALUE}]
　　[TDSQL_INCREMENT BY n]
　　[{TDSQL_CYCLE|TDSQL_NOCYCLE}]
```

## Creating a Sequence
```
create tdsql_sequence test.s1 start with 12 tdsql_minvalue 10 maxvalue 50000 tdsql_increment by 5 tdsql_nocycle
create tdsql_sequence test.s2 start with 12 tdsql_minvalue 10 maxvalue 50000 tdsql_increment by 1 tdsql_cycle
```
- The above SQL statements include six parameters: start value, minimum value, maximum value, increment, buffer size, and whether to cycle, all of which should be positive integers.
- The default values of these parameters are as follows: start value (1), minimum value (1), maximum value (LONGLONG_MAX-1), increment (1), and whether to cycle (0).

## Deleting a Sequence
```
drop tdsql_sequence test.s1
```

## Querying a Sequence
```
show tdsql_sequence
```

## Using a Sequence
#### Getting the next value
```
select tdsql_nextval(test.s2)
select next value for test.s2
```

```
mysql> select tdsql_nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select tdsql_nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 13 |
+----+
| 13 |
+----+
1 row in set (0.00 sec)

mysql> select next value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.01 sec)
```

#### Using nextval in INSERT and other statements
```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(tdsql_nextval(test.s2),3);
Query OK, 1 row affected (0.01 sec)

mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
| 14 |    3 |
+----+------+
2 rows in set (0.00 sec)
```

The last value is needed to join relevant data. If it has never been obtained with the `nextval` command, 0 will be returned.
```
select tdsql_lastval(test.s1)
select tdsql_previous value for test.s1;
```

```
mysql> select tdsql_lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

Set the next value for the sequence, which must be greater than the current value; otherwise, 0 will be returned.
```
select tdsql_setval(test.s2,1000,bool use)  // `use` is 1 by default, indicating that the value of 1,000 has been used and will not be included next time. If this is 0, the next return will start from 1,000.
```

If the next value of the sequence is smaller than the current value, the system will make no response.
```
mysql> select tdsql_nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select tdsql_setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+
```

If the next value set is larger than the current value, the current value will be successfully returned.
```
mysql> select tdsql_setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select tdsql_nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```

Forcibly set the next sequence value (you can set a value smaller than the current value).
```
select tdsql_resetval(test.s2,1000)
```

If the forced setting is successful, the set value will be returned, from which the next sequence value will start.
```
mysql> select tdsql_resetval(test.s2,14);
+----+
| 14 |
+----+
| 14 |
+----+
1 row in set (0.00 sec)

mysql> select tdsql_nextval(test.s2);
+----+
| 14 |
+----+
| 14 |
+----+
1 row in set (0.01 sec)
```

Note that some sequence keywords are prefixed with `TDSQL_`:
>?If the `oldstyle` configuration item is enabled, the proxy will be compatible with the standard `Sequence` keyword; that is, the `TDSQL_` prefix can be omitted for the keyword.
>
```
 TDSQL_CYCLE
 TDSQL_INCREMENT
 TDSQL_LASTVAL  
 TDSQL_MINVALUE 
 TDSQL_NEXTVAL  
 TDSQL_NOCACHE  
 TDSQL_NOCYCLE  
 TDSQL_NOMAXVALUE
 TDSQL_NOMINVALUE
 TDSQL_PREVIOUS 
 TDSQL_RESTART  
 TDSQL_REUSE    
 TDSQL_SEQUENCE 
 TDSQL_SETVAL   
```

