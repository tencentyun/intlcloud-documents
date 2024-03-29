
## 操作场景
容器服务 TKE 为用户提供了开箱即用的审计仪表盘。在集群开启集群审计功能后，TKE 将自动为该集群配置审计总览、节点操作总览、K8S 对象操作概览、聚合检索仪表盘。还支持用户自定义配置过滤项，同时内置 CLS 的全局检索，方便用户观测和检索各类集群操作，以便于及时发现和定位问题。




## 功能介绍
审计检索中配置了五个大盘，分别是“审计总览”、“节点操作总览”、“K8S对象操作概览”、“聚合检索”、“全局检索”。请按照以下步骤进入“审计检索”页面，开始使用对应功能：
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)。
2. 开启集群审计功能，详情请参见 [集群审计](https://intl.cloud.tencent.com/document/product/457/38338)。
3. 选择导航栏左侧**日志管理 > 审计日志**，进入“审计检索”页面。


### 审计总览
当您想观测整个集群 APIserver 操作时，可在“审计总览”页面设置过滤条件，查看核心审计日志的汇总统计信息，并展示一个周期内的数据对比。例如，核心审计日志的统计数、分布情况、重要操作趋势等。

您还可在该页面中查看更多统计信息，如下所示：
- 核心审计日志的统计数仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/72e7e252cb3bf2eaa643ad06cee0f3a4.png)
- 分布情况仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/5495968f3f4e4ee78c24e987903dc32c.png)
- 重要操作趋势仪表盘：
![](https://qcloudimg.tencent-cloud.cn/raw/960434920930f2528443a4f103eef372.png)





### 节点操作总览
当您需要排查节点相关问题时，可在“节点操作总览”页面设置过滤条件，查看各类节点操作相关的仪表，包括 create、delete、patch、update、封锁、驱逐等。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/150055420c58fa2c1e0d7f64bf278b63.png)

### K8S 对象操作概览
当您需要排查 K8S 对象（例如某个工作负载）的相关问题时，可在 “K8S 对象操作概览”页面设置过滤条件，查看各类 K8S 对象的操作概览、对应的操作用户、相应的审计日志列表，以查找更多的细节。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/9bd056c529943cd18a19f392898cc004.png)

### 聚合检索
当您想观测某个维度下审计日志的分布趋势，可在“聚合检索”页面设置过滤条件，查看各类重要操作的时序图。纬度包括操作用户、命名空间、操作类型、状态码、资源类型以及相应的审计日志列表。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/6132572a50dd7375dedbad453ec2c62d.png)

### 全局检索
全局检索仪表盘中内嵌了 CLS 的检索分析页面，方便用户在容器服务控制台 也能快速检索全部审计日志。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/28de4f8e3478c859f8ce53088e5ee580.png)


### 基于仪表盘配置告警

您可以通过以上预设的仪表盘配置告警，达到您所设置的条件则触发告警。操作详情如下：
1. 单击需要配置告警的仪表盘右侧的**快速添加告警**。
2. 在 **[日志服务控制台](https://console.cloud.tencent.com/cls/)**>**告警策略** 中新建告警策略。详情可参见 [配置告警策略](https://intl.cloud.tencent.com/document/product/614/39574)。

