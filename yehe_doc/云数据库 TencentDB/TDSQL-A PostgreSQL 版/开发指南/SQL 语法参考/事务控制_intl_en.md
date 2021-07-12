A transaction is a sequence of database operations that access and possibly manipulate various data items. These operations are either all executed or not executed at all. A transaction is an indivisible unit of work. It consists of all database operations performed between its beginning and end.
A transaction has two purposes:
- It provides a method for a database operation sequence to recover from failure to normal state and a method for the database to maintain consistency even in exceptional state.
- When multiple applications access the database concurrently, an isolation method can be provided between them to prevent mutual interference with each other's operations.

## Transaction Properties
Transactions have the ACID Properties as detailed below:
- Atomicity: all operations in the transaction are indivisible in the database, that is, either all are completed or all are not executed.
- Consistency: for several transactions executed in parallel, the execution result must be consistent with the result of serial execution in a certain order.
- Isolation: the execution of the transaction is not interfered by other transactions, and the intermediate results of the transaction execution must be transparent to other transactions.
- Durability: for any committed transaction, the system must ensure that the transaction's changes to the database are not lost, even if the database fails.

The ACID properties of transactions are implemented by a relational database management system (DBMS). The DBMS uses logs to ensure the atomicity, consistency, and durability of transactions. The log records the updates made by the transaction to the database. If an error occurs during the execution of a transaction, you can undo the updates made to the database by the transaction according to the log, so that the database is rolled to the initial state before the transaction is executed.

For transaction isolation, the DBMS uses a lock mechanism to achieve. When multiple transactions update the same data in the database at the same time, only the transaction holding the lock is allowed to update the data, and other transactions must wait until the previous transaction releases the lock before they have the opportunity to update the data.

## Transaction Isolation
The SQL standard defines four levels of transaction isolation. The most strict is Serializable, which is defined by the standard in a paragraph which says that any concurrent execution of a set of Serializable transactions is guaranteed to produce the same effect as running them one at a time in some order. The other three levels are defined in terms of phenomena, resulting from interaction between concurrent transactions, which must not occur at each level. The standard notes that due to the definition of Serializable, none of these phenomena are possible at that level.

The phenomena which are prohibited at various levels are:
**Dirty read**
A transaction reads data written by a concurrent uncommitted transaction.

**Nonrepeatable read**
A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).

**Phantom read**
A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently committed transaction.

**Serialization anomaly**
The result of successfully committing a group of transactions is inconsistent with all possible orderings of running those transactions one at a time.

| **Isolation Level** | **Dirty Read** | **Nonrepeatable Read** | **Phantom Read** | **Serialization Anomaly** |
| ------------ | -------- | -------------- | -------- | -------------- |
| Read uncommitted     | Allowed     | Possible           | Possible     | Possible           |
| Read committed     | Not possible   | Possible           | Possible     | Possible           |
| Repeatable read     | Not possible   | Not possible         | Allowed     | Possible           |
| Serializable     | Not possible   | Not possible         | Not possible   | Not possible         |

When you declare a transaction, you can request any of the four standard transaction isolation levels. Currently, the read uncommitted mode of TDSQL-A for PostgreSQL behaves like read committed, and read committed and repeatable read have been implemented.

## Transaction Control
### Starting transaction
You can use the `START TRANSACTION` or `BEGIN` syntax to start a transaction and declare the transaction isolation level and read/write mode when starting it.
Sample code:
```
postgres=# START TRANSACTION;
START TRANSACTION
```
Or:
```
postgres=# BEGIN;
BEGIN
```
Or:
```
postgres=# START TRANSACTION ISOLATION LEVEL REPEATABLE READ;
START TRANSACTION
```
Or:
```
postgres=# BEGIN WORK ISOLATION LEVEL READ COMMITTED; 
BEGIN
```

### Committing transaction
Process #1 accesses:
```
postgres=# BEGIN;
BEGIN
postgres=# DELETE FROM tdapg WHERE id=5;
DELETE 1
postgres=#
postgres=# SELECT * FROM tdapg ORDER BY id;
 id |  nickname  
----+---------------
 1 | hello tdapg
 2 | tdapg good
 3 | tdapg good
 4 | tdapg default
```

TDSQL-A for PostgreSQL fully supports ACID properties. If you start another connection query before committing a transaction, you will see five records, which is the implementation of isolation and multi-version view of TDSQL-A for PostgreSQL, as shown below:
Process #2 accesses:
```
postgres=# SELECT * FROM tdapg ORDER BY id;
 id |  nickname  
----+---------------
 1 | hello tdapg
 2 | tdapg good
 3 | tdapg good
 4 | tdapg default
 5 | tdapg swap
(5 rows)
```

Process #1 submits the data:
```
postgres=# COMMIT;
COMMIT
```

Process #2 queries data again, and the committed data can be seen, which indicates that the data is at the `read committed` level.
```
postgres=# SELECT * FROM tdapg ORDER BY id;
 id |  nickname  
----+---------------
 1 | hello tdapg
 2 | tdapg good
 3 | tdapg good
 4 | tdapg default
(4 rows)
```

### Rolling back transaction
```
postgres=# BEGIN;
BEGIN
postgres=# DELETE FROM tdapg WHERE id IN (3,4);
DELETE 2
postgres=# SELECT * FROM tdapg;
 id | nickname  
----+-------------
 1 | hello tdapg
 2 | tdapg good
(2 rows)

postgres=# ROLLBACK;
ROLLBACK
```

After `ROLLBACK`, the data has recovered to the state before the transaction starts:
```
postgres=# SELECT * FROM tdapg;
 id |  nickname  
----+---------------
 1 | hello tdapg
 2 | tdapg good
 3 | tdapg good
 4 | tdapg default
(4 rows)
```
