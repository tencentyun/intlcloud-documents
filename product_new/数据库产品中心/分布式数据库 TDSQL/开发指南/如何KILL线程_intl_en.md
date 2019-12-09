When you use the database to run certain statements, deadlock may occur with no response due to large data volume. At this time, you need to kill the query statement that is consuming resources by running the following command:
```
	KILL [CONNECTION | QUERY] thread_id
```
Note: As TDSQL consists of multiple database nodes (sets), you must use "/*" to pass through the [custom comments](https://intl.cloud.tencent.com/document/product/1042/33373) to kill a thread successfully.
```
	/*sets:set_1*/kill 890346;
```
As TDSQL consists of multiple database nodes (sets), you can use the `/*sets:set_1*/SHOW PROCESSLIST` statement to view the running threads, and use the `KILL thread_id` statement to terminate a thread.

> Query set_ID. Go to Distributed Database > Management > Node Management in the console, or use the `/*proxy*/show status;` command.

```
	mysql> /*sets:set_524110864_1*/show processlist;
	+---------+--------+-----------------------+------+---------+------+-------+--------------------------------------------+----------+------------------+
	| Id      | User   | Host                  | db   | Command | Time | State | Info                                       | Progress | info             |
	+---------+--------+-----------------------+------+---------+------+-------+--------------------------------------------+----------+------------------+
	| 1072003 | vitosu | 13.26.12.18:4859 | NULL | Sleep   |  189 |       | NULL                                       |    0.000 | set_1524110864_1 |
	| 1072132 | vitosu | 13.26.12.18:4823 | NULL | Query   |    0 | init  | /*sets:set_524110864_1*/ show processlist |    0.000 | set_1524110864_1 |
	+---------+--------+-----------------------+------+---------+------+-------+--------------------------------------------+----------+------------------+

	mysql> /*sets:set_524110864_1*/kill 1072003;
	Query OK, 0 rows affected (0.03 sec)
```
If your business has many threads and you cannot accurately determine which transactions have not been committed, you can use a similar SQL to query thread ID (for example):
```
	SELECT
	  it.trx_id AS trx_id,
	  it.trx_state AS trx_state,
	  it.trx_started AS trx_started,
	  it.trx_mysql_thread_id AS trx_mysql_thread_id,
	  CURRENT_TIMESTAMP - it.trx_started AS RUN_TIME,
	  pl.user AS USER,
	  pl.host AS HOST,
	  pl.db AS db,
	  pl.time AS trx_run_time,
	  pl.INFO as INFO
	FROM
	  information_schema.INNODB_TRX it,
	  information_schema.processlist pl
	WHERE
	  pl.id=it.trx_mysql_thread_id
	ORDER BY RUN_TIME DESC LIMIT 10;
```
If your business has many threads and you cannot accurately determine which transactions are in the status of lock wait, you can use a similar SQL to query thread ID (for example):
```
	SELECT
	r.trx_id waiting_trx_id,
	r.trx_mysql_thread_id waiting_thread,
	TIMESTAMPDIFF( SECOND, r.trx_wait_started, CURRENT_TIMESTAMP ) wait_time,
	r.trx_query waiting_query,
	l.lock_table waiting_table_lock,
	b.trx_id blocking_trx_id,
	b.trx_mysql_thread_id blocking_thread,
	SUBSTRING( p. HOST, 1, INSTR(p. HOST, ':') - 1 ) blocking_host,
	SUBSTRING(p. HOST, INSTR(p. HOST, ':') + 1) blocking_port,
	IF (p.COMMAND = 'Sleep', p.TIME, 0) idel_in_trx,
	b.trx_query blocking_query FROM information_schema.INNODB_LOCK_WAITS w INNER JOIN information_schema.INNODB_TRX b ON b.trx_id = w.blocking_trx_id INNER JOIN information_schema.INNODB_TRX r ON r.trx_id = w.requesting_trx_id INNER JOIN information_schema.INNODB_LOCKS l ON w.requested_lock_id = l.lock_id LEFT JOIN information_schema. PROCESSLIST p ON p.ID = b.trx_mysql_thread_id ORDER BY wait_time DESC;
```

> Risk warning: After a large transaction is killed, it needs to be rolled back, which may lead to long wait time if the data volume is high. In this case, you can click master-slave switch in the console to promote the slave as the master for quick business restoration. **However, please note that when using an async or strong sync (downgradable) replication scheme, due to the delay of master-slave data sync, some data may get lost or disordered. Please perform master-slave switch with caution.**
