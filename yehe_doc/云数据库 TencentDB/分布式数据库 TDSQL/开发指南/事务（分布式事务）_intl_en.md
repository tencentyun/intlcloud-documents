
If you want to view or download the full set of development documents, please see [Development Guide for TDSQL](https://intl.cloud.tencent.com/document/product/1042/33352).

As the data manipulated by a transaction usually spans across multiple physical nodes, in a distributed database, a similar scheme is called a distributed transaction. TDSQL (v5.7 and above) supports distributed transactions that are imperceptible to the client, so that they can be used by the business just like standalone transactions. Below are some examples:
```
	begin; // Start a transaction
	delete
	update // Manipulate data (cross-set operations are supported)
	select
	insert
	commit; // Commit a transaction
```

SQL statements are added to query the information of a specific transaction:
- `select gtid()` is used to get the `gtid` (globally unique identifier of a transaction) of the current distributed transaction. Null will be returned if the transaction is not a distributed one.
Format of `gtid`:
'Gateway ID'-'random value of gateway'-'serial number'-'timestamp'-'partition number', such as c46535fe-b6-dd-595db6b8-25
- `select gtid_state("gtid")` is used to get the status of `gtid`. Below are possible results:
  - "COMMIT", indicating that the transaction has been or will be eventually committed.
  - "ABORT", indicating that the transaction will be eventually rolled back.
  - Null. The transaction status will be cleared after one hour, so there are two possibilities:
  a). For query after one hour, it indicates that the transaction status has been cleared.
  b). For query within an hour, it indicates that the transaction will be eventually rolled back.
When a commit operation times out or fails, you should wait a few seconds before calling the API to query the transaction status.

- OPS commands:
	xa recover: sends the `xa recover` command to the backend set and summarizes the results.
	xa lockwait: displays the wait relationship of the current distributed transaction (you can use the `dot` command to convert the output to a wait-for graph).
	xa show: shows the distributed transactions that are currently running on the gateway.

#### Notes
Distributed transactions in TDSQL adopt a two-phase commit protocol (2PC) with an isolation level configured as "read committed", "repeatable read", or "serializable".
