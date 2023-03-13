TencentDB for MySQL을 사용하면 병렬 쿼리 실행 계획과 계획의 스레드를 볼 수 있으므로 데이터베이스에서 병렬 쿼리가 어떻게 적용되는지 명확하게 파악하고 문제를 신속하게 해결할 수 있습니다.
본문은 병렬 쿼리를 보기 위한 두 가지 일반적인 방법을 설명합니다.

## 옵션1: EXPLAIN 문 사용
**샘플 SQL 문:**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
이 샘플은 일반적인 리포트 작업인 TPC-H Q1의 단순화된 버전입니다.

**EXPLAIN 문:**
```
EXPLAIN  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**쿼리 결과:**
```
MySQL [tpch100g]> explain SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '1998-09-02' GROUP BY l_returnflag, l_linestatus ORDER BY l_returnflag, l_linestatus;
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
| id | select_type | table       | partitions | type | possible_keys | key  | key_len | ref  | rows      | filtered | Extra                                                     |
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
|  1 | SIMPLE      | lineitem    | NULL       | ALL  | i_l_shipdate  | NULL | NULL    | NULL | 593184480 |    50.00 | Parallel scan (4 workers); Using where; Using temporary   |
|  1 | SIMPLE      | <sender1>   | NULL       | ALL  | NULL          | NULL | NULL    | NULL |         0 |     0.00 | Send to (<receiver1>)                                     |
|  1 | SIMPLE      | <receiver1> | NULL       | ALL  | NULL          | NULL | NULL    | NULL |         0 |     0.00 | Receive from (<sender1>); Using temporary; Using filesort |
+----+-------------+-------------+------------+------+---------------+------+---------+------+-----------+----------+-----------------------------------------------------------+
3 rows in set, 1 warning (0.00 sec)
```
**EXPLAIN format=tree:**
```
EXPLAIN format=tree query  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**쿼리 결과:**
```
MySQL [tpch100g]> explain format=tree SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '1998-09-02' GROUP BY l_returnflag, l_linestatus ORDER BY l_returnflag, l_linestatus\G
*************************** 1. row ***************************
EXPLAIN: -> Sort: lineitem.L_RETURNFLAG, lineitem.L_LINESTATUS
    -> Table scan on <temporary>
        -> Final Aggregate using temporary table
            -> PX Receiver (slice: 0; workers: 1)
                -> PX Sender (slice: 1; workers: 4)
                    -> Table scan on <temporary>
                        -> Aggregate using temporary table
                            -> Filter: (lineitem.L_SHIPDATE <= DATE'1998-09-02')  (cost=65449341.10 rows=296592240)
                                -> Parallel table scan on lineitem  (cost=65449341.10 rows=593184480)

1 row in set (0.00 sec)
```
상기 결과에서 알 수 있듯이:
- 병렬 쿼리 계획은 컴퓨팅을 위해 4개의 작업자 스레드에 명령문을 할당합니다.
- 집계 작업은 사용자와 병렬 스레드에 의해 각각 실행되는 두 개의 세그먼트로 나뉩니다.
- lineitem 테이블에는 병렬 스캔 연산자가 사용됩니다.
- EXPLAIN format=tree query는 기존 EXPLAIN보다 더 잘 작동합니다.

## 옵션2: 스레드 목록에서 보기
show processlist 명령의 결과는 실행 중인 스레드를 표시합니다. 현재 전체 연결 수뿐만 아니라 비정상적인 쿼리 문을 식별하기 위한 연결 상태도 볼 수 있습니다.
show processlist 명령을 기반으로 TencentDB for MySQL은 병렬 쿼리와 관련된 스레드만 표시하고 관련 없는 스레드를 필터링하는 독점적인 show parallel processlist 문을 제공합니다.
**샘플 SQL 문:**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
이 샘플은 일반적인 보고 작업인 TPC-H Q1의 단순화된 버전입니다.
**show processlist 쿼리 결과:**
```
mysql> show processlist;
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
| Id     | User        | Host            | db        | Command | Time  | State      | Info                                                                                                 |
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
|      7 | tencentroot | 127.0.0.1:49238 | NULL      | Sleep   |     0 |            | NULL                                                                                                 |
|     11 | tencentroot | 127.0.0.1:49262 | NULL      | Sleep   |     0 |            | NULL                                                                                                 |
|     13 | tencentroot | 127.0.0.1:49288 | NULL      | Sleep   |     1 |            | NULL                                                                                                 |
| 237062 | tencentroot | localhost       | tpch100g  | Query   |    24 | Scheduling | SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '199 |
| 237107 | tencentroot | localhost       | NULL      | Query   |     0 | init       | show processlist                                                                                     |
+--------+-------------+-----------------+-----------+---------+-------+------------+------------------------------------------------------------------------------------------------------+
6 rows in set (0.00 sec)
```
**show parallel processlist 쿼리 결과:**
```
mysql> show parallel processlist;
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
| Id     | User        | Host      | db       | Command | Time | State       | Info                                                                                                 |
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
| 237062 | tencentroot | localhost | tpch100g | Query   |   18 | Scheduling  | SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty FROM lineitem WHERE l_shipdate <= '199 |
| 237110 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 0, task 1                                                                  |
| 237111 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 1, task 1                                                                  |
| 237112 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 2, task 1                                                                  |
| 237113 |             |           |          | Task    |   18 | Task runing | connection 237062, worker 3, task 1                                                                  |
+--------+-------------+-----------+----------+---------+------+-------------+------------------------------------------------------------------------------------------------------+
5 rows in set (0.00 sec)
```

상기 결과에서 알 수 있듯이:
- 병렬 쿼리 계획은 4개의 work 스레드에 쿼리를 할당합니다. user 스레드에는 데이터 항목이 하나만 있습니다(ID: 237062). SQL 문은 4개의 work 스레드로 푸시 다운됩니다. info에 표시된 대로 이 네 개의 스레드는 모두 task1을 실행하고 있습니다.
- 각 스레드를 정확하게 식별하고 찾을 수 있습니다.
- show processlist와 비교할 때 show parallel processlist는 병렬 쿼리의 실행 중인 모든 스레드를 정확하게 찾을 수 있으며 다른 스레드의 영향을 받지 않습니다.

## 관련 문서
- [병렬 쿼리 활성화/비활성화](https://www.tencentcloud.com/document/product/236/52512)
- [hint 문 제어](https://www.tencentcloud.com/document/product/236/53410)

