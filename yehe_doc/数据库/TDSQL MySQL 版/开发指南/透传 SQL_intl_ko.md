TDSQL for MySQL은 SQL 실행을 제한하는 SQL 구문을 구문 분석합니다. set에서 TDSQL이 아닌 MySQL에서 지원하는 SQL 문을 실행하려는 경우 SQL 문을 전달할 수 있습니다.
>?
>- proxy는 전달된 SQL 문을 구문 분석하지 않습니다. 두 set에 대한 통과 쓰기 작업인 경우 분산 트랜잭션을 사용하지 않으므로 극단적인 경우 불일치가 발생할 수 있습니다. 따라서 단일 쓰기 작업에서 하나의 set으로만 전달하는 것이 좋습니다.
>- 통과 구문이 적용되도록 하려면 MySQL에 연결할 때 -c 매개변수를 추가하십시오.


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

구체적인 구문:
- sets:set_1,set_2: SQL 문이 통과할 set을 지정하는 데 사용됩니다. set 이름은 `/*proxy*/show status`로 조회할 수 있습니다.
- sets:allsets: SQL 문이 모든 set로 전달될 것임을 나타냅니다.
- shardkey:10: SQL 문이 지정된 shardkey에 따라 set로 전달됨을 나타냅니다.
- shardkey_hash:10: 지정된 hash 값이 10인 set로 SQL 문을 전달함을 나타냅니다. shardkey_hash가 0으로 설정되면 SQL 문은 첫 번째 set로 전달됩니다.

