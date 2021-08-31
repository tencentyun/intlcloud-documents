The `LOCK TABLE` statement can get table-level locks and can only be used in a transaction block. Without the `UNLOCK TABLE` statement, the lock will be automatically released after the transaction ends. If you use the `LOCK` command to lock a table, the most strict mode `ACCESS EXCLUSIVE` will be used by default.
```
v3=# begin;
BEGIN
v3=# lock table t10;
LOCK TABLE
v3=# select relation::regclass,mode from pg_locks;
 relation |    mode
----------+---------------------
t10   | AccessExclusiveLock
```

## Table-Level Lock
**ACCESS SHARE**
The `SELECT` command acquires a lock of this mode on referenced tables. In general, any query that only reads a table and does not modify it will acquire this lock mode.

**ROW SHARE**
The `SELECT FOR UPDATE` and `SELECT FOR SHARE` commands acquire a lock of this mode on the target table(s) (in addition to `ACCESS SHARE` locks on any other tables that are referenced but not selected `FOR UPDATE/FOR SHARE`).

**ROW EXCLUSIVE**
The commands `UPDATE`, `DELETE`, and `INSERT` acquire this lock mode on the target table (in addition to `ACCESS SHARE` locks on any other referenced tables). In general, this lock mode will be acquired by any command that modifies data in a table.

**SHARE UPDATE EXCLUSIVE**
It is acquired by `VACUUM` (without `FULL`), `ANALYZE`, `CREATE INDEX CONCURRENTLY`, `CREATE STATISTICS`, `ALTER TABLE VALIDATE`, and certain `ALTER TABLE` variants.

**SHARE**
It is acquired by `CREATE INDEX` (without `CONCURRENTLY`).

**SHARE ROW EXCLUSIVE**
It is acquired by `CREATE COLLATION`, `CREATE TRIGGER`, and some forms of `ALTER TABLE`.

**EXCLUSIVE**
It is acquired by `REFRESH MATERIALIZED VIEW CONCURRENTLY`.

**ACCESS EXCLUSIVE**
It is acquired by the `ALTER TABLE`, `DROP TABLE`, `TRUNCATE`, `REINDEX`, `CLUSTER`, `VACUUM FULL`, and `REFRESH MATERIALIZED VIEW` (without `CONCURRENTLY`) commands. Many forms of `ALTER TABLE` also acquire a lock at this level (for more information, please see [ALTER TABLE](http://postgres.cn/docs/10/sql-altertable.html)). This is also the default lock mode for `LOCK TABLE` statements that do not specify a mode explicitly.

**Conflicting lock modes**
Locks will be blocked by and conflict with each other.
<table>
<thead><tr><th rowspan=2>Requested Lock Mode</th><th colspan=8>Existing Lock Mode</th></tr></thead>
<tbody><tr>
<td>-</td>
<td>ACCESS  SHARE</td>
<td>ROW SHARE</td>
<td>ROW  EXCLUSIVE</td>
<td>SHARE  UPDATE EXCLUSIVE</td>
<td>SHARE</td>
<td>SHARE ROW  EXCLUSIVE</td>
<td>EXCLUSIVE</td>
<td>ACCESS  EXCLUSIVE</td></tr>
<tr>
<td>ACCESS  SHARE</td>
<td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>X</td></tr>
<tr>
<td>ROW SHARE</td>
<td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>-</td><td>X</td><td>X</td></tr>
<tr>
<td>ROW  EXCLUSIVE</td>
<td>-</td><td>-</td><td>-</td><td>-</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
<tr>
<td>SHARE  UPDATE EXCLUSIVE</td>
<td>-</td><td>-</td><td>-</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
<tr>
<td>SHARE</td>
<td>-</td><td>-</td><td>X</td><td>X</td><td>-</td><td>X</td><td>X</td><td>X</td></tr>
<tr>
<td>SHARE ROW  EXCLUSIVE</td>
<td>-</td><td>-</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
<tr>
<td>EXCLUSIVE</td>
<td>-</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
<tr>
<td>ACCESS  EXCLUSIVE</td>
<td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr>
</tbody></table>

In addition to table-level locks, there are row-level locks. They do not affect data querying; they block only writers and lockers to the same row.

## Deadlock
In TDSQL-A for PostgreSQL, deadlocks will occur due to resource preemption by concurrently executed transactions. You can check all locked objects in a database in the `pg_locks` system view.
The use of explicit locking can increase the likelihood of deadlocks, wherein two (or more) transactions each hold locks that the other wants. You can manually end or use other methods to end a transaction so as to resolve the deadlock.

Query existing locks:
```
select pid,relation::regclass,mode from pg_locks where relation<>'pg_locks'::regclass::oid;
pid | relation |   mode
-----------+------------+-----------------
27577 | t4   | AccessShareLock
```
You can use the correlated subquery of the `pid` field in the `pg_locks` system view and the `pg_stat_activity` system view to query the information of transactions currently holding locks.
