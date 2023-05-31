
### Is TDSQL-C for MySQL compatible with open-source MySQL?
Yes. TDSQL-C for MySQL is fully compatible with MySQL 5.7 and 8.0.

### Which transaction isolation levels are supported?
TDSQL-C for MySQL supports two isolation levels: `READ_COMMITTED` (default) and `REPEATABLE_READ`. You can modify the `tx_isolation` parameter in **Parameter Settings** to change the transaction isolation level. For detailed directions, see [Setting Instance Parameters](https://www.tencentcloud.com/document/product/1098/44602).

### Is the binlog format different from the native format of MySQL?
There is no difference between them.

### Are performance schema and sys schema supported?
Yes.

### Are the collected table statistics different from those in open-source MySQL?
No. To ensure that the execution plans of read-write and read-only instances are consistent, every time the read-write instance updates the statistics, the change will be synced to read-only instances.No. To ensure that the execution plans of read-write and read-only instances are consistent, every time the read-write instance updates the statistics, the change will be synced to read-only instances.

### Does TDSQL-C for MySQL support XA transactions? Are there any differences in this regard between TDSQL-C for MySQL and open-source MySQL?
Yes, and there are no differences.

### Does TDSQL-C for MySQL support full-text indexing?
Yes.

### Is Percona Toolkit supported?
Yes. However, we recommend you use online DDL.

### Is gh-ost supported?
Yes. However, we recommend you use online DDL.
