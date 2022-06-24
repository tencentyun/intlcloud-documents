## Feature Description

The command word analysis feature performs statistical analysis on the number and latency of database access commands. Latency analysis helps you quickly find the most frequently used command, and command word analysis helps you further identify when the command is most frequently executed as well as its execution latency, which facilitates troubleshooting and performance optimization.

## Viewing Command Word Analysis

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. On the left sidebar, select **Performance Optimization**.
3. At the top of the **Performance Optimization** page of **DBbrain**, select the target instance in the **Instance ID** drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/ff8626c75f17a6d9e15edb0f2d57c290.png)
4. Select the **Latency Analysis** > **Command Word Analysis** tab and set the collection granularity to **5s**, **15s**, or **30s** as needed in the drop-down list next to **Auto-Refresh** in the top-right corner.
![img](https://qcloudimg.tencent-cloud.cn/raw/ed2f8767576c33f9ba83dded844d2e69.png)
5. (Optional) Quickly filter target command words in the drop-down list in the top-left corner.
![img](https://qcloudimg.tencent-cloud.cn/raw/ec02f05d8d4738840caca5cc2e3bea17.png)
6. Analyze the trend data of the command words.
   - **Real-time statistics**
     Real-time statistics are displayed by default, including the change trends of the following metrics: command requests, P99 execution latency, average execution latency, and max execution latency. For more information on metrics, see [Performance Trends](https://intl.cloud.tencent.com/document/product/239/47579).
     ![img](https://qcloudimg.tencent-cloud.cn/raw/5ad76583baba87b1cf92435ea8800d94.png)
   - **Historical data**
     Click **Historical** to view the statistics in the last 30 minutes, 6 hours, or 24 hours. You can also click <img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" /> in the time selection box to view the statistics in the last 2 days.
     ![img](https://qcloudimg.tencent-cloud.cn/raw/9fb14ac794b9e9b7334eb8b381a07621.png)
