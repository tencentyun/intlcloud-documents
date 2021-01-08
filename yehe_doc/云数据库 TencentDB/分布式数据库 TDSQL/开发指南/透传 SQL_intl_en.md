TDSQL for MySQL parses SQL syntax, which restricts SQL execution. If you want to execute SQL statements supported by MySQL but not by TDSQL on a set, you can pass through the SQL statements.
>?When a SQL statement is passed through, the proxy will not parse it, so if it is a passthrough write operation to two sets, distributed transactions will not be used, which may cause inconsistency in extreme cases. Therefore, we recommend that you pass through only to one set during one write operation.
>
```
MySQL [test]> repair table test.t1;
ERROR 664 (HY000): Proxy ERROR:SQL is too complex, only applicable to noshard table: Shard table do not support repair
MySQL [test]> /*sets:allsets*/repair table test.t1;
+---------+--------+----------+----------+------------------+
| Table   | Op     | Msg_type | Msg_text | info             |
+---------+--------+----------+----------+------------------+
| test.t1 | repair | status   | OK       | set_1544429866_3 |
| test.t1 | repair | status   | OK       | set_1544429718_1 |
+---------+--------+----------+----------+------------------+
2 rows in set (0.01 sec)
```

Syntax:
- sets:set_1,set_2: it is used to specify the sets to which SQL statements will be passed through. The set name can be queried by `/*proxy*/show status`.
- sets:allsets: it indicates that SQL statements will be passed through to all sets.
- shardkey:10: it indicates that SQL statements will be passed through to the set according to the specified shardkey.
- shardkey_hash:10: it indicates that SQL statements will be passed through to the set where its specified hash value is 10. If `shardkey_hash` is set to 0, SQL statements will be passed through to the first set.

