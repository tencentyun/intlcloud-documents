## Description
Tencent Cloud offers database auditing for TencentDB MySQL instances. With this feature, database access and SQL statement execution information, including the start time of statement execution, the number of scanned rows, lock wait time, CPU time, client IP, username, and SQL statement, will be audited, assisting enterprises in risk management and data protection.

## Use cases
This feature is suitable for the use cases where risky database behaviors (such as SQL injection and abnormal operation) need to be recorded and alarmed.

## Impact on the performance
There are two audit modes: sync and async. Sync audit synchronously records all audit logs with an average impact of less than 6% on instance performance. But async audit has almost no impact (less than 3%, to be precise), which is industry-leading.

## Notes
For more information on how to enable TencentDB for MySQL audit, see [Enabling TencentDB for MySQL Audit](https://www.tencentcloud.com/document/product/1102/41311).

