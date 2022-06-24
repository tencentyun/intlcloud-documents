## 功能描述

DBbrain 延迟分析功能， 提供延时洞察功能，对数据库所有请求命令进行延时统计，精确到毫秒级别的延迟耗时监控，帮助您排查 Redis 数据库故障和性能降低的原因。 

## 查看延迟分析

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在左侧导航栏，选择**诊断优化**。
3. 在**数据库智能管家 DBbrain** 的**诊断优化**页面上方，**实例 ID** 的下拉列表选择需查看的实例。
![](https://qcloudimg.tencent-cloud.cn/raw/02e73372d964981f933626bf8180d9d5.png)
4. 选择**延迟分析**页签，并在右上方**自动刷新**后面的下拉列表中设置采集粒度，支持5秒、15秒、30秒。
![](https://qcloudimg.tencent-cloud.cn/raw/7023aa77e2c232a3b786db5beccbc4a2.png)
5. 查看延迟分析监控数据。
 - **实时监控**
默认以曲线图形式展示实时监控的数据的变化。
![](https://qcloudimg.tencent-cloud.cn/raw/7b0c8db8eddf5c875874ab8232c3c0b5.png)
 - **查看历史数据**
单击**历史**，查看历史时间段的监控数据。
    - 直接选择**近30分钟**、**近6小时**、**近24小时**，查看对应时间段的监控数据。
    - 在时间选择框，单击<img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" />，可查看**近2天**内的监控数据。
![](https://qcloudimg.tencent-cloud.cn/raw/2dee6fbb207be502616d82cda3c1c2c5.png)

## 解读延迟分析统计数据 
### 总请求/CPU 使用率
展示数据库实例每秒总请求次数的变化趋势，及其对应的 CPU 使用率的变化。可快速识别出请求数偏大时 CPU 使用率达到的数值。

### 延迟水位线
展示数据库请求执行延迟相关的3个关键指标的变化趋势，并展示耗时时长 Top5 的耗时命令 。
- **P99执行时延**：99%延迟耗时时长的变化趋势。
- **平均执行时延**：请求耗时平均时长的变化趋势。
- **最大执行时延**：请求耗时最大时延的变化趋势。

### 延迟分布
以条形图的形式统计数据库不同延迟耗时时段的命令次数。延迟时长分段包括：0ms - 1ms、1ms - 2ms、5ms - 10ms、10ms - 50ms、50ms - 200ms、大于200ms。下图中统计出0ms - 1ms 耗时的命令次数为2703次。
![](https://qcloudimg.tencent-cloud.cn/raw/84a7bbae2ce2801dca4146ff6efe3ba7.png)

### 访问命令
以柱状图形式统计数据库访问命令的命中次数。下图统计了 auth、get 命令的访问次数。单击命令字分析页签，可查看各个访问命令的统计数据，具体信息，请参见 [命令字分析](https://intl.cloud.tencent.com/document/product/239/47574)。
![img](https://qcloudimg.tencent-cloud.cn/raw/1369ba9f3e3500338fa925f1be9470a4.png)

