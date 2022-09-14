
## 操作场景
TKEServerless集群为用户提供了开箱即用的审计仪表盘。在集群开启集群审计功能后，TKEServerless集群将自动为该集群配置审计总览、K8S 对象操作概览、聚合检索仪表盘。还支持用户自定义配置过滤项，同时内置 CLS 的全局检索，方便用户观测和检索各类集群操作，以便于及时发现和定位问题。




## 功能介绍

审计检索中配置了四个大盘，分别是“审计总览”、“K8S 对象操作概览”、“聚合检索”、“全局检索”。请按照以下步骤进入“审计检索”页面，开始使用对应功能：
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)。
2. 开启集群审计功能，详情请参见 [集群审计](https://intl.cloud.tencent.com/document/product/457/46742)。
3. 选择导航栏左侧**集群运维** > **审计日志**，进入“审计检索”页面。


### 审计总览

当您需要观测整个集群 APIserver 操作时，可在“审计总览”页面设置过滤条件，查看核心审计日志的汇总统计信息，并展示一个周期内的数据对比。例如，核心审计日志的统计数、分布情况、重要操作趋势等。
在过滤项中，您可根据自己需求进行个性化配置，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0553485fcf7b6f0f4548d25609779fd6.png)


您还可在该页面中查看更多统计信息，如下所示：
- 核心审计日志的统计数仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/979bbae8a39e8f180514bd7242f0b094.png)  
- 分布情况仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/1660c2afee1a72edb42e5afa4fbd6398.png)  
- 重要操作趋势仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/682a3ac6ca022a66205fd0d6503f0e24.png)






### K8S 对象操作概览

当您需要排查 K8S 对象（例如某个工作负载）的相关问题时，可在切换至**K8S 对象操作概览**页签，在此页面设置过滤条件，查看各类 K8S 对象的操作概览、对应的操作用户、相应的审计日志列表，以查找更多的细节。
如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0045848f54c9e86e503cebfa98e06b9a.png)

### 聚合检索

当您需要观测某个维度下审计日志的分布趋势，可在“聚合检索”页面设置过滤条件，查看各类重要操作的时序图。纬度包括操作用户、命名空间、操作类型、状态码、资源类型以及相应的审计日志列表。
如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5a66f20bca612308c6f05aff0ecd537e.png)

### 全局检索

全局检索仪表盘中内嵌了 CLS 的检索分析页面，方便用户在容器服务控制台 也能快速检索全部审计日志。
如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/3db084804e5b7fc20d53766cc6fdeb94.png)

### 基于仪表盘配置告警

您可以通过以上预设的仪表盘配置告警，达到您所设置的条件则触发告警。具体操作如下：

1. 在需要配置告警的仪表盘右侧中单击**<img src="https://main.qcloudimg.com/raw/77e0007d25c9724e5b2f05ab3ff8f95a.png" width="2.5%">**，在下拉菜单中选择**快速添加告警**。
2. 配置告警策略详细步骤，请参见 [配置告警策略](https://intl.cloud.tencent.com/document/product/614/39574)。

