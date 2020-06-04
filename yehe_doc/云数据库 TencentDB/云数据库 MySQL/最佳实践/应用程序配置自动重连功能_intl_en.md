This document describes the impact of seconds-level disconnection during instance switch and how to configure automatic reconnection.
## Background
In TencentDB for MySQL, when you are [adjusting database instance specification](https://intl.cloud.tencent.com/document/product/236/19707) or [upgrading database engine](https://intl.cloud.tencent.com/document/product/236/8126), the master instance is hanging due to overload, or the hardware fails, etc., the instance may need to switch, causing a seconds-level disconnection.

If application automatic reconnection is not configured, the application will disconnect after the master/slave switch, which affects the access of business.

We recommend that you configure automatic reconnection for applications and switch instances during [maintenance window](https://intl.cloud.tencent.com/document/product/236/10929).


## Configuring Automatic Reconnection
To avoid application connection errors due to master/slave switch, we recommend that you configure automatic reconnection for TencentDB for MySQL applications by setting the connection pool parameters, i.e., `connectTimeOut` and `socketTimeOut`.
Set parameter values according to different business scenarios. For OLTP (On-Line Transaction Processing) business scenarios, both parameters should be set to 20 seconds.
>
>- `connectTimeOut`: timeout period for the application to establish a TCP connection with the database server. It is recommended to set the parameter to a value greater than the database server response time.
>- `socketTimeOut`: timeout period for waiting a response after packets are sent over the TCP connection. It is recommended to set the parameter to the maximum execution time for a single SQL statement.

