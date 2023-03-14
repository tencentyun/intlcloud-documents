TencentDB for MySQLは、並列クエリーの実行スケジュールの確認、および並列クエリースケジュールを実行しているスレッドの確認をサポートします。並列クエリーがデータベースでに安定して動作する方法を明確に理解でき、また、並列クエリーの実行中に問題が発生した場合に、問題をすばやく特定することができます。
このドキュメントでは、並列クエリーを表示する2つの一般的な方法を紹介します。

## 方法1：EXPLAINステートメントの使用
**SQLステートメントの例：**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
この例は、TPC-H Q1の単純化された形式で、典型的なレポート操作です。

**実行スケジュールのプリントステートメント（EXPLAIN）：**
```
EXPLAIN  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**結果のクエリー:**
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
**ツリー実行スケジュールのプリントステートメント（EXPLAIN format=tree）:**
```
EXPLAIN format=tree query  SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
**結果のクエリー:**
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
上記の結果から、次のことが分かります：
- 並列クエリースケジュールは、ステートメントを4つのワーカースレッドに配分して計算します。
- 集計計算を上下に分割し、ユーザースレッドと並列スレッドを別々に実行します。
- lineitemテーブルに対して並列スキャン演算子を使用します。
- インスタンスにおいて、ツリー実行スケジュールのプリント（EXPLAIN format=tree query）は、従来の実行スケジュールのプリント（EXPLAIN）と比較して、効果がより優れています。

## 方法2：スレッドリストの表示
show processlistコマンドの出力結果には、実行中のスレッドが表示されます。現在のすべての接続数を表示できるだけでなく、現在の接続ステータスを表示して、問題のあるクエリーステートメントなどを特定することもできます。
show processlistコマンドに基づいて、TencentDB for MySQLは、show parallel processlistステートメントを自社開発しています。スレッド中の非並列クエリースレッドをフィルタリングするのに役立ちます。このコマンドラインを使用すると、並列クエリーに関連するスレッドのみが表示されます。
**SQLステートメントの例：**
```
SELECT l_returnflag, l_linestatus, sum(l_quantity) as sum_qty
FROM lineitem
WHERE l_shipdate <= '1998-09-02'
GROUP BY l_returnflag, l_linestatus
ORDER BY l_returnflag, l_linestatus;
```
この例は、TPC-H Q1の単純化された形式で、典型的なレポート操作です。
**show processlistのクエリー結果：**
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
**show parallel processlistのクエリー結果：**
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

上記の結果から、次のことが分かります：
- 上記クエリーは、並列スケジュールによって4つのworkスレッドに配分して実行されます。userは1行のみに表示され、ID 237062がユーザースレッドであることを示し、SQLステートメントの実行スケジュールを次の4つのworkスレッドにプッシュダウンして実行し、info列から、この4つのワーカースレッドはすべてtask1を実行していることが分かります。
- すべてのスレッドをクエリーでき、正確に特定しています。
- show parallel processlistはshow processlistと比較して、他のスレッドの影響を受けることなく、並列クエリーを実行するすべてのスレッドを正確にクエリーできます。

##  関連ドキュメント
- [並列クエリーのオン・オフ](https://www.tencentcloud.com/document/product/236/52512)
- [Hintステートメント制御](https://www.tencentcloud.com/document/product/236/53410)

