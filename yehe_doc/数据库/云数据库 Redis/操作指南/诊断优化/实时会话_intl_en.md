## Feature Description

The real-time session feature focuses on the two key metrics of database proxy node CPU utilization and client connection quantity. It dynamically displays their change trends and continuously collects the data of database sessions, access sources, and active connection quantity.
Through real-time session, you can quickly identify the CPU utilization of current sessions and efficiently locate logic issues about database session connections that are difficult to detect manually. 
![](https://qcloudimg.tencent-cloud.cn/raw/0899c31f9f0cd666b82f1ad8d7d80e33.png)

## Viewing Real-Time Session Statistics

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/b661dae4775781a1f4de646a6144ccf0.png)
4. Click the **Real-Time Session** tab and select the target **proxy ID** in the drop-down list in the top-left corner of the **Performance Monitoring** view based on the trend of **CPU Utilization** or **Connections**.
In the top-right corner of the **Performance Monitoring** view, select the collection granularity of the monitoring data in the drop-down list next to **Auto-Refresh**, which is **5s** by default and can also be set to **15s** or **30s**.
![](https://qcloudimg.tencent-cloud.cn/raw/ff05601ae1825f9cb29f39e153661061.png)
5. View the real-time session details.
 - In the **Performance Monitoring** section, you can view the change trends of the current proxy node connections and CPU utilization.
 - In the **Session Statistics** section, you can view the database's statistics of current access sources, total connections, and active connections.

## One-Click Kill

You can click **One-Click Kill** to quickly kill all sessions.
![](https://qcloudimg.tencent-cloud.cn/raw/04affaaa71dc4e707f304db1773803fe.png)

