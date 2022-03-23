
This document describes the version updates of the TencentDB for MySQL database proxy.

## Viewing Database Proxy Version
You can view the version in **Overview** > **Proxy Version** on the [Database Proxy](https://intl.cloud.tencent.com/document/product/236/42052) tab.
![](https://qcloudimg.tencent-cloud.cn/raw/6868726aa0bdb77251d41979120986ae.png)

## Version Upgrade Description
| Version | Description |
|---------|---------|
| 1.1.2 | **Updated features**<br>1. Supported MySQL 8.0.<br>2. Supported the connection pool feature at the connection level, which is useful in scenarios where non-persistent connections to the database are frequently established. The database proxy will save connections and reuse them during subsequent connection establishments.<br>3. Supported the reconnection feature for read-only instances. In persistent connection scenarios, when a read-only instance is restarted or added, the database proxy will automatically establish a connection and restore routing to it.<br>4. Updated the internal memory management mechanism to reduce the memory usage.<br>**Fixed issues**<br>1. Fixed the issue where the client connection persisted after the backend connection was closed due to timeout.<br>2. Fixed the issue where the internal cache might cause excessively rapid increase of the memory utilization.<br>3. Fixed the occasional issue where packets in an incorrect format were returned. |
| 1.0.1 | **Updated features**<br>1. Supported MySQL 5.7.<br>2. Supported read/write separation.<br>3. Supported read weight assignment in read/write separation.<br>4. Supported the configuration of source-replica replication delay threshold. Routing to a read-only instance will be stopped if its delay exceeds the thresholds and will be recovered after it drops below the threshold. If the source-replica replication is interrupted, disconnected read-only instances will be removed directly.<br>5. Supported the configuration of the least number of read-only instances. When read-only instances are removed, if the number is set to N, at least N instance(s) will be retained for routing.<br>6. Supported the failover configuration, which is enabled by default. If it is disabled and the read weight of the source instance is 0, after all read-only instances are removed, an error will be reported for read requests. If failover is enabled and the read weight of the source instance is not 0, requests will be routed to the source instance.<br>7. Supported using the HINT syntax to specify router nodes. |

