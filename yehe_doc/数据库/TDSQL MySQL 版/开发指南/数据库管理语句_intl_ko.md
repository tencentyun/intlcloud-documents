## 상태 쿼리
SQL을 통해 proxy의 설정 및 상태를 볼 수 있습니다. 현재 지원되는 명령은 다음과 같습니다.
- `/*proxy*/help;`
- `/*proxy*/show config;`
- `/*proxy*/show status;`

>?MySQL 클라이언트에 로그인하는 경우 mysql -hxxx.xxx.xxx.xxx -Pxxxx -uxxx -pxxx -c와 같이 코드에 `-c`를 추가합니다.

예시는 다음과 같습니다:
```
	mysql> /*proxy*/help;
	+-----------------------+-------------------------------------------------------+
	| command               | description                                           |
	+-----------------------+-------------------------------------------------------+
	| show config           | show config from conf                                 |
	| show status           | show proxy status,like route,shardkey and so on       |
	| set sys_log_level=N   | change the sys debug level N should be 0,1,2,3        |
	| set inter_log_level=N | change the interface debug level N should be 0,1      |
	| set inter_time_open=N | change the interface time debug level N should be 0,1 |
	| set sql_log_level=N   | change the sql debug level N should be 0,1            |
	| set slow_log_level=N  | change the slow debug level N should be 0,1           |
	| set slow_log_ms=N     | change the slow ms                                    |
	| set log_clean_time=N  | change the log clean days                             |
	| set log_clean_size=N  | change the log clean size in GB                       |
	+-----------------------+-------------------------------------------------------+
	10 rows in set (0.00 sec)
```

```
	mysql> /*proxy*/show config;
	+-----------------+--------------------+
	| config_name     | value              |
	+-----------------+--------------------+
	| version         | V2R120D001         |
	| mode            | group shard        |
	| rootdir         | /shard_922         |
	| sys_log_level   | 0                  |
	| inter_log_level | 0                  |
	| inter_time_open | 0                  |
	| sql_log_level   | 0                  |
	| slow_log_level  | 0                  |
	| slow_log_ms     | 1000               |
	| log_clean_time  | 1                  |
	| log_clean_size  | 1                  |
	| rw_split        | 1                  |
	| ip_pass_through | 0                  |
	+-----------------+--------------------+
	14 rows in set (0.00 sec)
```

```
	mysql> /*proxy*/show status;
	+-----------------------------+------------------------------------------------------------------------------+
	| status_name                 | value                                                                        |
	+-----------------------------+------------------------------------------------------------------------------+
	| cluster                     | group_1499858910_79548                                                       |
	| set_1499859173_1:ip         | 10.49.118.165:5025;10.175.98.109:5025@1@IDC_4@0,10.231.23.241:5025@1@IDC_2@0 |
	| set_1499859173_1:hash_range | 0---31                                                                       |
	| set_1499911640_3:ip         | 10.49.118.165:5026;10.175.98.109:5026@1@IDC_4@0,10.231.23.241:5026@1@IDC_2@0 |
	| set_1499911640_3:hash_range | 32---63                                                                      |
	| set                         | set_1499859173_1,set_1499911640_3                                            |
```

한편 proxy는 proxy에 의해 수정된 SQL 문을 표시하여 Explain의 반환된 결과를 향상시킵니다.
```
	mysql> explain select * from test1;
	+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
	| id   | select_type | table | type | possible_keys | key  | key_len | ref  | rows | Extra | info                                    |
	+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
	|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_2,explain select * from shard.test1 |
	|    1 | SIMPLE      | test1 | ALL  | NULL          | NULL | NULL    | NULL |   16 |       | set_1,explain select * from shard.test1 |
	+------+-------------+-------+------+---------------+------+---------+------+------+-------+-----------------------------------------+
	2 rows in set (0.03 sec)
```
