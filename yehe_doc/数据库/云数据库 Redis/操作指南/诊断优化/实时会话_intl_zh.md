## 功能描述

实时会话聚焦数据库实例 Proxy 节点 CPU 使用率与客户端的连接数量这两项关键指标，持续动态展示这两项关键指标的变化趋势，且持续统计数据库会话、访问来源、活跃连接数等数据。
运维、管理人员可通过实时会话快速识别当前会话 CPU 资源的使用情况，高效定位数据库会话连接相关人工难以发现的逻辑问题。 
![](https://qcloudimg.tencent-cloud.cn/raw/0899c31f9f0cd666b82f1ad8d7d80e33.png)

## 查看实时会话统计数据

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在左侧导航栏，选择**诊断优化**。
3. 在**数据库智能管家 DBbrain** 的**诊断优化**页面上方，在**实例 ID** 的下拉列表选择需查看的实例。
![](https://qcloudimg.tencent-cloud.cn/raw/b661dae4775781a1f4de646a6144ccf0.png)
4. 单击**实时会话**页签，在**性能监控**视图左上方的下拉列表中，可根据 **CPU使用率**的趋势图或**连接数**的趋势图选择需分析的 **Proxy ID**。
在**性能监控**视图右上方，**自动刷新**后面的下拉列表中选择监控数据的采集粒度，默认为**5秒**，支持5秒、15秒、30秒。
![](https://qcloudimg.tencent-cloud.cn/raw/ff05601ae1825f9cb29f39e153661061.png)
5. 查看实时会话详细数据。
 - 在**性能监控**区域，可查看当前 Proxy 节点的连接数及其 CPU 使用率的变化趋势。
 - 在**会话统计**区域，可查看数据库当前访问来源、总连接数、活跃连接数的统计信息。

## 一键 Kill

一键 Kill 将一键 Kill 掉所有的会话。
![](https://qcloudimg.tencent-cloud.cn/raw/04affaaa71dc4e707f304db1773803fe.png)

