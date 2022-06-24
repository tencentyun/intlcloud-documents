## 功能描述

命令字分析，针对数据库访问命令的数量及其时延进行分析统计。延迟分析可快速找到访问次数高的命令，命令字分析可进一步分析该命令数量执行高的具体时间，及其执行时延情况，辅助排障定位，优化性能。

## 查看命令字分析

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在左侧导航栏，选择**诊断优化**。
3. 在**数据库智能管家 DBbrain** 的**诊断优化**页面上方，在**实例 ID** 的下拉列表选择需查看的实例。
![](https://qcloudimg.tencent-cloud.cn/raw/ff8626c75f17a6d9e15edb0f2d57c290.png)
4. 选择**延迟分析** > **命令字分析**页签，并在右上方**自动刷新**后面的下拉列表中设置采集粒度，支持5秒、15秒、30秒。
![img](https://qcloudimg.tencent-cloud.cn/raw/ed2f8767576c33f9ba83dded844d2e69.png)
5. （可选）在左上角的下拉列表中，可过滤命令字，快速查找需分析的命令字。
![img](https://qcloudimg.tencent-cloud.cn/raw/ec02f05d8d4738840caca5cc2e3bea17.png)
6. 分析命令字的变化趋势数据。
   - **实时统计**
     默认实时统计数据，包括：命令请求数、P99执行时延、平均执行时延、最大执行时延指标的变化趋势。指标详情可参见 [性能趋势](https://intl.cloud.tencent.com/document/product/239/47579) 的性能指标。
     ![img](https://qcloudimg.tencent-cloud.cn/raw/5ad76583baba87b1cf92435ea8800d94.png)
   - **历史数据**
     单击**历史**，可直接查看近30分钟、近6小时、近24小时的统计数据。在时间选择框，单击<img src="https://qcloudimg.tencent-cloud.cn/raw/a1438740099d1baedaf57020fb2e397b.png" style="zoom: 50%;" />，也可查看近2天的统计数据。
     ![img](https://qcloudimg.tencent-cloud.cn/raw/9fb14ac794b9e9b7334eb8b381a07621.png)
