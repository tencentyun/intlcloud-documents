This document describes the impact of seconds-level disconnection during instance switch and how to configure automatic reconnection.
## Background
In case of [adjusting database instance specification](https://intl.cloud.tencent.com/document/product/236/19707) or [upgrading database engine](https://intl.cloud.tencent.com/document/product/236/8126), the source instance is overloaded and hanging, hardware fails, etc., the instance may need to switch, causing disconnection for few seconds.

If automatic reconnection is not configured, the application will disconnect after the source-replica switch and normal business access will be affected.

We recommend that you configure automatic reconnection for applications and switch instances during the [maintenance window](https://intl.cloud.tencent.com/document/product/236/10929).


## Configuring Automatic Reconnection
To avoid application connection exceptions due to source-replica switch, we recommend that you configure automatic reconnection for TencentDB for MySQL applications by configuring the connection pool parameters, i.e., `connectTimeOut` and `socketTimeOut`.
Configure parameter values according to business scenarios. For OLTP (Online Transaction Processing) business scenarios, both parameters should be configured as 20 seconds.
>?
>- `connectTimeOut`: Timeout period for the application to establish a TCP connection with the database server. We recommend that you configure this parameter with a value greater than the response time between the application and the database server.
>- `socketTimeOut`: Timeout period while waiting for a response after packets are sent over the TCP connection. We recommend that you configure this parameter to the maximum execution time for a single SQL statement.

