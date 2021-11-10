Connection protection keeps the connection intact between the client and the proxy when the proxy is disconnected from the backend database, so in cases such as when the backend database has an exception, the proxy will not be affected.

If the proxy is disconnected from the database while executing SQL, the proxy will close all connections related to the SQL (except the connection between itself and the client) and display an error:
```c++
ER_PROXY_TRANSACTION_ERROR // Transaction in progress
ER_PROXY_CONN_BROKEN_ERROR // No transaction in progress
```

#### Solutions
- If the proxy is disconnected from the backend database and your session is in a "transaction in progress" status, this can be fixed as follows (all the error codes below are ER_PROXY_TRANSACTION_ERROR):
![](https://main.qcloudimg.com/raw/2698586724f600292b4af375192fdd5d.png)

- If the proxy is disconnected from the backend database and your session is in an "XA transaction in progress" status, this can be fixed as follows (all the error codes below are ER_PROXY_TRANSACTION_ERROR):
![](https://main.qcloudimg.com/raw/f927b13caa1157e6262dae2cfdd9cea0.png)

#### Timeout Configuration
>?If the proxy disconnects from the backend database during the execution of a transaction and the transaction fails to be rolled back before the timeout period elapses, the proxy will disconnect from the client.
>
The timeout parameter is configured in the proxy configuration file as follows:
```json
<server_close timeout="60"/>
```
