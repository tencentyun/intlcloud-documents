## Impala failed to start as the data volume increased

### Background

When there is too much metadata (such as hundreds of databases or tens of thousands of tables) in Impala, Impala needs to broadcast such metadata to all nodes when starting, with a timeout period of 10 seconds by default. If there is a large amount of metadata and the broadcasting is easy to trigger, you can set `-statestore_subscriber_timeout_seconds=100` in the `/data/Impala/conf/impalad.flgs` launch configuration file to fix this problem.

### Troubleshooting

Generally, when this issue occurs, the following content will appear in the Impala log at `/data/emr/impala/logs`:
```
Connection with state-store lost
Trying to re-register with state-store
```

## Impala queries are slow due to a low configuration

Although Impala is not an in-memory database, it is still necessary to allocate more physical memory to Impala when dealing with large tables or high volumes of data. You are generally recommended to use a memory of 128 GB or more and allocate 80% of it to the Impala process.

## A SELECT statement failed

Possible reasons:
1. Timeout was caused by a performance, capacity, or network issue with a particular node. View the Impala log to identify the node and check whether the problem persists after changing the node network.
2. Automatic cancellation of queries was caused due to excessive memory usage by `join` queries. Check whether the `join` statement is appropriate or increase the server memory.
3. The way how a node generates native code to process a specific `WHERE` clause in a query was incorrect, such as server instructions that are not supported by the processor that can generate a specific node. If the error message in the log indicates that the cause is an invalid instruction, please consider disabling native code generation before trying a query again.
4. The input data format is incorrect, such as text data files with very long lines or delimiters that do not match the characters specified in the `FIELDS TERMINATED BY` clause of the `CREATE TABLE` statement. Check whether there is extra-long data and whether correct delimiters are used in the `CREATE TABLE` statement.

## Setting a limit on the memory usage of queries

```
[localhost:27001] > set mem_limit=3000000000;
MEM_LIMIT set to 3000000000
[localhost:27001] > select 5;
Query: select 5
+---+ |5 | +---+ |5 | +---+
[localhost:27001] > set mem_limit=3g;
MEM_LIMIT set to 3g
[localhost:27001] > select 5;
Query: select 5
+---+ |5 | +---+ |5 | +---+
[localhost:27001] > set mem_limit=3gb;
MEM_LIMIT set to 3gb
[localhost:27001] > select 5;
+---+
|5 | +---+ |5 | +---+
[localhost:27001] > set mem_limit=3m;
MEM_LIMIT set to 3m
[localhost:27001] > select 5;
+---+
|5 |
+---+
|5 |
+---+
[localhost:27001] > set mem_limit=3mb; MEM_LIMIT set to 3mb [localhost:21000] > select 5;
+---+ |5 | +---+
```

