TDSQL supports the SEQUENCE keyword, whose syntax is compatible with MariaDB and Oracle. Sequences must be globally incremented and unique in the distributed architecture. This document describes how to use SEQUENCE.

To create a sequence, you need the `CREATE SEQUENCE` system permission. The syntax to create a sequence is as follows:
```
　　CREATE SEQUENCE sequence name
　　[INCREMENT BY n]
　　[START WITH n]
　　[{MAXVALUE/ MINVALUE n| NOMAXVALUE}]
　　[{CYCLE|NOCYCLE}]
　　[{CACHE n| NOCACHE}];
```

>?Currently, sequences must be globally incremented and unique in the distributed architecture, resulting in a relatively low performance, so they are only suitable for scenarios with low concurrency.

## Creating a Sequence
Sample code:
```
create sequence test.s1 start with 12 minvalue 10 maxvalue 50000  increment by 5  nocycle 
create sequence test.s2 start with 12 minvalue 10 maxvalue 50000  increment by 1  cycle 
```
Parameters include start value, minimum value, maximum value, increment, and whether to cycle.

## Deleting a Sequence
Sample code:
```
drop sequence test.s1
```
Current constraint: all parameters should be positive integers.

## Viewing a Sequence
Sample code:
```
show create sequence test.s1
```

## Using a Sequence
#### Manipulating the sequence of a table
```
select nextval(test.s1)
select next value for test.s1
```

Sample code:
```
mysql> select nextval(test.s1);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.18 sec)

mysql> select nextval(test.s2);
+----+
| 12 |
+----+
| 12 |
+----+
1 row in set (0.13 sec)

mysql> select nextval(test.s1);
+----+
| 17 |
+----+
| 17 |
+----+
1 row in set (0.01 sec)

mysql> select nextval(test.s2);
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

NEXTVAL can be used in SELECT or other statements.
```
mysql> select * from test.t1;
+----+------+
| a  | b    |
+----+------+
| 11 |    2 |
+----+------+
1 row in set (0.00 sec)

mysql> insert into test.t1(a,b) values(nextval(test.s2),3);
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

#### Querying the last value
If NEXTVAL has not been used to query data, 0 will be returned.
```
select lastval(test.s1)
select previous value for test.s1;
```

Sample code:
```
mysql> select lastval(test.s1);
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)

mysql> select previous value for test.s1;
+----+
| 22 |
+----+
| 22 |
+----+
1 row in set (0.00 sec)
```

#### Setting the next value
The next value must be incremented or else 0 will be returned.
```
select setval(test.s2,1000,bool use)  // "use" is 1 by default, indicating that the value of 1,000 has been used and the next value will not be 1,000. If "use" is 0, the next value will start from 1,000.
```

If the next value is decremented, 0 will be returned.
```
mysql> select nextval(test.s2);
+----+
| 15 |
+----+
| 15 |
+----+
1 row in set (0.01 sec)

mysql> select setval(test.s2,10);
+---+
| 0 |
+---+
| 0 |
+---+
1 row in set (0.03 sec)

mysql> select nextval(test.s2);
+----+
| 16 |
+----+
| 16 |
+----+
```

If the next value is incremented, the value you just set will be successfully returned.
```
mysql> select setval(test.s2,20);
+----+
| 20 |
+----+
| 20 |
+----+
1 row in set (0.02 sec)
mysql> select nextval(test.s2);
+----+
| 21 |
+----+
| 21 |
+----+
1 row in set (0.01 sec)
```


Note that the following sequence keywords are prefixed with `TDSQL_`:
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
