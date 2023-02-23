Database audit is a professional, efficient, and comprehensive database audit service independently developed by Tencent Cloud for monitoring database security in real time. It can record the activities of TencentDB instances in real time, manage the compliance of database operations with fine-grained audit, and alert risky database behaviors.
TDSQL-C for MySQL provides database audit capabilities to help you record accesses to databases and executions of SQL statements, so you can manage risks and improve the database security. In addition, it allows you to customize frequent and infrequent access storage types to greatly reduce the costs of database audit.

## Use cases
- Database audit offers a compliance audit basis for enterprises to pass CCP Level 3 and other industry-specific audits.
- Database audit helps enterprises record, analyze, and track database security incidents such as maloperations.
- Database audit improves the efficiency and accuracy in various database scenarios such as performance optimization and fault locating.

## Billing
Database audit is billed by the stored log size for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.
For detailed pricing, see [Database Audit Billing Overview](https://www.tencentcloud.com/document/product/1098/52146).

## Supported versions
Database audit in TDSQL-C for MySQL currently supports MySQL 5.7 and 8.0.

## Strengths
Database audit in TDSQL-C for MySQL has a rich set of features, including full audit, rule-based audit, frequent/infrequent access storage, and long-term audit log retention. It has the following strengths:

**Data integrity during collection**
Database audit in TDSQL-C for MySQL is implemented based on the kernel plugin of MySQL. The execution of each SQL statement will undergo a complete process from connection, parsing, analysis, rewrite, and optimization to execution, return, audit, and release. After database audit is enabled and connected to the TDSQL-C for MySQL server, each SQL statement will be audited during execution. If audit fails, the statement was not executed successfully. If a statement is executed successfully, it will definitely be successfully audited. A SQL request connection will be released only after audit, which guarantees the integrity of the collected data.

**Data reliability during collection**
Database audit in TDSQL-C for MySQL captures data synchronously from MySQL's own execution layer instead of capturing data asynchronously. Therefore, the audited SQL statements and the SQL statements executed in TDSQL-C for MySQL are synced in real time and consistent with each other. This ensures that the captured data is always correct, guaranteeing the reliability of the collected data.

**Data tampering protection**
The audit control system has a behavior monitoring mechanism. When someone exploits a vulnerability to launch attacks, vulnerability scan can monitor intrusions in real time by capturing relevant session information and sending alarms. When someone manipulates the audit data, all access requests will be logged for you to check which user accesses the data from which source IP address and thus discover high-risk access operations in time. The database audit service also supports account/role-based authentication, so that different data read/write permissions can be granted to users with different roles, which solves problems caused by account sharing. When someone performs a high-risk operation, a tampering alarm will be triggered in real time for prompt risk discovery, analysis, tracking, and prevention.

**Data integrity during transfer**
When audit data is processed at the transfer linkage layer after being collected, it will be verified in multiple dimensions, including cyclic redundancy check (CRC), globally unique ID check, linkage MQ redundancy check, and Flink-based stream processing, guaranteeing the data integrity during transfer.

**Data integrity during storage**
The database audit system encrypts the stored audit log files, so that only users with the encryption certificate access can view audit logs. This effectively prevents internal data leaks caused by plaintext storage and data thefts by high-privileged users, fundamentally eliminating the risks of audit data leaks and guaranteeing the integrity of the stored data.
