This document describes the connection pool feature. The TencentDB for MySQL proxy supports the session-level connection pool feature. It can effectively solve the problem of excessively high database instance loads caused by frequent establishments of new non-persistent connections.

## Prerequisites
You have [enabled the database proxy](https://intl.cloud.tencent.com/document/product/236/42052).

## Background
#### Session-level connection pool
![](https://qcloudimg.tencent-cloud.cn/raw/f708a404a68e16abb747e1088ce14ba6.png)
The session-level connection pool is applicable to non-persistent connection scenarios.

The session-level connection pool is used to reduce the instance load caused by frequent establishments of new non-persistent connections. If a client connection is closed, the system will determine whether the current connection is idle, and if so, the system will put it into the proxy connection pool and retain it for a short period of time.
When the client initiates a new connection, if the connection pool has an available connection, the connection can be used directly to reduce the database connection overheads; otherwise, a new connection will be established as usual.

>?
>- The session-level connection pool does not reduce the number of concurrent connections to the database, but it can reduce the overheads of the main thread of TencentDB for MySQL by lowering the speed for connecting the application to the database, so as to better process business requests. However, idle connections in the connection pool will occupy your connection quantity temporarily.
>- The session-level connection pool cannot be used to solve the problem of connection heap caused by a large number of slow SQL queries, which must first be solved by yourself.

## Notes
- Currently, the connection pool feature does not support setting different permissions for different IPs under the same account, as that may cause a permission error during connection reuse. For example, if `mt@test123` has `database_a` permissions, while `mt@test456` does not, a permission error may occur when you enable the connection pool.
- The connection pool feature is for the database proxy instead of the client. You don't need to use the connection pool of the database proxy if your client already supports it.

