Database audit is a professional, efficient, and comprehensive database audit service independently developed by Tencent Cloud for monitoring database security in real time. It can record the activities of TencentDB instances in real time, manage the compliance of database operations with fine-grained audit, and alert risky database behaviors.
TencentDB for MySQL provides database audit capabilities to help you record accesses to databases and executions of SQL statements, so you can manage risks and improve the database security. In addition, it allows you to customize frequent and infrequent access storage types to greatly reduce the costs of database audit.

## Use Cases
- **Audit risks**
     - Difficulty in tracing and locating security breaches due to incomplete audit logs.
     - Inability to meet the requirements defined by China's Cybersecurity Classified Protection Certification (Level 3).
     - Inability to meet the requirements defined by industry-specific information security compliance documents.

- **Administrative risks**
     - Business system security risks caused by faulty, non-compliant, and unauthorized operations of technical personnel.
     - Faulty and malicious operations and tampering by third-party development and maintenance personnel.
     - Excessive permissions granted to the super admin, which cannot be audited and monitored.

- **Technical challenges**
     - Database system SQL injections that maliciously pull data from databases and tables.
     - Inability to troubleshoot the sudden increase of database requests that are not slow queries.

## Product Billing
Database audit is billed by the stored log size for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.
For detailed pricing, see [Database Audit Billing Overview](https://www.tencentcloud.com/document/product/236/52083).

## Supported Versions
TencentDB for MySQL audit is supported for two-node and three-node instances on MySQL 5.6 20180101 or above, MySQL 5.7 20190429 or above, and MySQL 8.0 20210330 or above.

## Advantages
### Full audit
Database Audit fully records the accesses to databases and executions of SQL statements to meet your audit requirements and ensure database security as much as possible.
### Rule-based audit
Rule-based audit records access requests to the database and SQL statement executions according to the custom audit rule.
### Efficient audit
Different from non-embedded audit mode, Database Audit records TencentDB operations through the embedded database kernel plugin, which makes the records more accurate.
### Long-term retention
Database Audit allows you to retain logs persistently according to your business needs to meet regulatory compliance requirements.
### Architecture characteristics
Database audit adopts the multi-point deployment architecture to guarantee the service availability. It records logs in a streaming manner to prevent tampering and retains them in multiple copies to ensure the data reliability.

## Data Security
- **Data integrity during collection**
Database audit in TencentDB for MySQL is implemented based on the kernel plugin of MySQL. The execution of each SQL statement will undergo a complete process from connection, parsing, analysis, rewrite, and optimization to execution, return, audit, and release. After database audit is enabled and connected to the TencentDB for MySQL server, each SQL statement will be audited during execution. If audit fails, the statement was not executed successfully. If a statement is executed successfully, it will definitely be successfully audited. A SQL request connection will be released only after audit, which guarantees the integrity of the collected data.

- **Data reliability during collection**
Database audit in TencentDB for MySQL captures data synchronously from MySQL's own execution layer instead of capturing data asynchronously. Therefore, the audited SQL statements and the SQL statements executed in TencentDB for MySQL are synced in real time and consistent with each other. This ensures that the captured data is always correct, guaranteeing the reliability of the collected data.

- **Data tampering protection**
The audit control system has a behavior monitoring mechanism. When someone exploits a vulnerability to launch attacks, vulnerability scan can monitor intrusions in real time by capturing relevant session information and sending alarms. When someone manipulates the audit data, all access requests will be logged for you to check which user accesses the data from which source IP address and thus discover high-risk access operations in time. The database audit service also supports account/role-based authentication, so that different data read/write permissions can be granted to users with different roles, which solves problems caused by account sharing. When someone performs a high-risk operation, a tampering alarm will be triggered in real time for prompt risk discovery, analysis, tracking, and prevention.

- **Data integrity during transfer**
When audit data is processed at the transfer linkage layer after being collected, it will be verified in multiple dimensions, including cyclic redundancy check (CRC), globally unique ID check, linkage MQ redundancy check, and Flink-based stream processing, guaranteeing the data integrity during transfer.

- **Data integrity during storage**
The database audit system encrypts the stored audit log files, so that only users with the encryption certificate access can view audit logs. This effectively prevents internal data leaks caused by plaintext storage and data thefts by high-privileged users, fundamentally eliminating the risks of audit the data leakage and guaranteeing the integrity of the stored data.