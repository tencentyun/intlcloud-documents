## Index-based Query
After the global index feature is enabled, TcaplusDB supports the field query, provided that the field in the query condition must have global index created.
The fields in an aggregate query also require global index.
An index-based query returns up to 3,000 results.

### Supported statements
#### Query conditions
The following query conditions are supported, including `=, >, >=, <, <=, !=, between, in, not in, like, not like, and, or`.

>!
>- The two values of `between` are included in the range. For example, if you use `between 1 and 100`, both 1 and 100 are inclusive. In other words, the query range should be [1,100].
>- The `like` query supports fuzzy matching. The wildcard % matches zero or multiple characters, while the wildcard _ matches one character.

```
tcaplus> select * from pb_generic_index_shardingkey where openid>10 and tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
 
tcaplus> select * from pb_generic_index_shardingkey where openid between 1 and 300  and tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
 
tcaplus> select * from pb_generic_index_shardingkey where openid>10 or tconndid<1000;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
 
 
total 5 records
```


#### Paginated query
The paginated query `limit offset` is supported.

>!The paginated query must use `limit offset`. Neither `limit 1` or `limit 0,1` can be used.

```
tcaplus> select * from pb_generic_index_shardingkey where openid>10 limit 3 offset 0;
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |other_property                           |items|lockid   |pay|id_uint32|id_int32|
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|[{"key":1,"value":1},{"key":2,"value":2}]|-    |[1,2,3,4]|-  |1        |1       |
+------+---------+--------+-------+-----------+-----------------------------------------+-----+---------+---+---------+--------+
```


#### Aggregate query
The following aggregate query functions are supported, including `sum, count, max, min, avg`.
>!
>- The aggregate query does not support `limit offset`.
>- Currently, only the `count` function can be used with `distinct`. For example, `select count(distinct(a)) from table where a > 1000`.

```
tcaplus> select sum(openid), count(*), max(openid), avg(openid) from pb_generic_index_shardingkey where openid>10 ;
1010,5,204,202
```


#### Specified field query
The values of specified fields can be queried.
>?You can also query nested fields in the Protobuf table. For example, `select field1.field2.field3, a, b from table where a > 1000`.
>
```
tcaplus> select svrid,gamesvrid from pb_generic_index_shardingkey where openid>10 or tconndid<1000;
+------+---------+--------+-------+-----------+
|openid|timekey  |tconndid|svrid  |gamesvrid  |
+------+---------+--------+-------+-----------+
|204   |"timekey"|204     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|203   |"timekey"|203     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|202   |"timekey"|202     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|200   |"timekey"|200     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
|201   |"timekey"|201     |"svrid"|"gamesvrid"|
+------+---------+--------+-------+-----------+
 
 
total 5 records
```



### Unsupported SQL statements
#### Using an aggregate query with non-aggregate query
```
select *, a, b from table where a > 1000;

select sum(a), a, b from table where a  > 1000;

select count(*), * from table where a  > 1000;
```

#### Query by `order by`
```
select * from table where a > 1000 limit 100 offset 0;
```

#### Query by `group by`
```
select * from table where a > 1000 group by a;
```

#### Query by `having`
```
select sum(a) from table where  a > 1000 group by a having sum(a) > 10000;
```

#### Multi-table query
```
select * from table1 where table1.a > 1000 and table1.a = table2.b;
```

#### Nested SELECT query
```
select * from table where a > 1000 and b in (select b from table where b < 5000);
```

#### AS query
```
select sum(a) as sum_a from table where a > 1000;
```

#### Other queries not supported
- JOIN
- UNION
- Queries like `select a+b from table where a > 1000`
- Queries like `select * from table where a+b > 1000`
- Queries like `select * from table where a >= b`
- Others

