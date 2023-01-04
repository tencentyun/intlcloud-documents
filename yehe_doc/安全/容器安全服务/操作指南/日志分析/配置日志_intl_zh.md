### 日志接入
1. 在 [日志分析页面](https://console.cloud.tencent.com/tcss/report/logAnalysis)，单击页面上方的**日志配置** > **日志接入**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/591023877529d1fd3de595450a075d32.png" style="zoom:150%;" />
2. 在日志接入页面，支持对容器 bash 日志、容器启动审计日志和 Kubernetes API 审计日志是否开启采集进行配置。在“是否接入日志”列开启开关，即可对该类日志进行采集。关闭按钮，即不对该类日志进行采集。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ce7ae2e19001dfd524204a805dfd5da.png" style="zoom:67%;" />
3. 在日志接入页面，单击已接入资产列的**编辑**，即可配置采集日志的节点范围。勾选需要采集日志的主机节点，单击**提交**后，配置生效。
<img src="https://qcloudimg.tencent-cloud.cn/raw/759665d44460178215aece46b090b409.png" style="zoom:50%;" />

### 日志清理
1. 在 [日志分析页面](https://console.cloud.tencent.com/tcss/report/logAnalysis)，单击页面上方的**日志配置** > **日志清理**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b0719cd3e937163ff2aaec00ebea057a.png" style="zoom:150%;" />
2. 在日志清理页面，支持用户按百分比或存储天数清理日志。
  - 按百分比清理日志：当日志存储量达到用户配置百分比时，开始清理历史日志，清理到用户配置的清理百分比。
  - 按存储天数清理日志：当日志存储天数达到用户配置数值时，开始清理历史日志，仅保留用户配置天数的日志。
>? 两种日志清理方式同时生效，当任一情况满足时即开始日志清理。

<img src="https://qcloudimg.tencent-cloud.cn/raw/eca863417a4044d07d474c357abba6c1.png" style="zoom:67%;" />
