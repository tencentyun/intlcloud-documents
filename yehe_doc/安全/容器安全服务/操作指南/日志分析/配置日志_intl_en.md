### Log collection
1. On the [**Log Analysis**](https://console.cloud.tencent.com/tcss/report/logAnalysis) page, click **Log configuration** > **Log collection** at the top.
<img src="https://qcloudimg.tencent-cloud.cn/raw/591023877529d1fd3de595450a075d32.png" style="zoom:150%;" />
2. On the **Log collection** tab, toggle on or off the **Enabled** switch to enable or disable the collection of container bash logs, container startup audit logs, and Kubernetes API audit logs.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce7ae2e19001dfd524204a805dfd5da.png" style="zoom:67%;" />
3. On the **Log collection** tab, click **Edit** in the **Accessed assets** column to configure the node scope for log collection. Select the servers for log collection and click **Submit**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/759665d44460178215aece46b090b409.png" style="zoom:50%;" />

### Log cleanup
1. On the [**Log Analysis**](https://console.cloud.tencent.com/tcss/report/logAnalysis) page, select **Log configuration** > **Log cleanup** at the top.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b0719cd3e937163ff2aaec00ebea057a.png" style="zoom:150%;" />
2. On the **Log cleanup** tab, clear logs by percentage or storage period.
  - Clear logs by percentage: When the log storage volume reaches the configured percentage, historical logs are cleared until the configured percentage.
  - Clear logs by storage period: When the log storage period reaches the configured value, historical logs are cleared, and only those within the configured storage period are retained.
>? The two cleanup methods take effect at the same time, which means log cleanup starts when either of the two conditions is met.

<img src="https://qcloudimg.tencent-cloud.cn/raw/eca863417a4044d07d474c357abba6c1.png" style="zoom:67%;" />
