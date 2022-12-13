
## 操作场景
容器服务 TKE 为用户提供了开箱即用的事件仪表盘。在集群开启事件存储功能后，TKE 将自动为集群配置各类事件总览大盘和异常事件的聚合检索分析仪表盘。还支持用户自定义配置过滤项，同时内置 CLS 的事件全局检索，实现在容器服务控制台 全面观测、查找、分析、定位问题的能力。


## 功能介绍

事件检索中配置了三个大盘，分别是“事件总览”、“异常事件聚合检索”、“全局检索”。请按照以下步骤进入“事件检索”页面，开始使用对应功能：
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)。
2. 开启“事件存储功能”，详情请参见 [事件存储](https://intl.cloud.tencent.com/document/product/457/30686)。
3. 选择导航栏左侧**集群运维** > **事件检索**，进入“事件检索”页面。


### 事件总览

在“事件总览”页面，可根据时间、命名空间、级别、原因、资源类型、资源对象等维度过滤事件，查看核心事件的汇总统计信息，并展示一个周期内的数据对比。例如，事件总数及分布情况、节点异常、Pod OOM、重要事件趋势等仪表盘以及异常 TOP 事件列表。
在过滤项中，您可根据自己需求进行个性化配置。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/IJ7i823_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212105810.png)

您还可在该页面中查看更多统计信息，如下所示：
- 事件总数及级别分布情况，异常事件的原因、对象分布情况检索如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/kGL9521_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212105928.png)
- 各类常见事件的汇总信息检索如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/A83s522_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212110409.png)
- 事件趋势及异常 TOP 事件列表检索如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XQH9575_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212110432.png)


### 异常事件聚合检索
在“异常事件聚合检索”页面设置过滤条件，查看某个时间段内各类异常事件的 reason 和 object 分布趋势。在趋势下方展示了可供搜索的异常事件列表，帮助您快速定位到问题。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HfQB934_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212111210.png)

### 全局检索
全局检索仪表盘中内嵌了 CLS 的检索分析页面，方便用户在容器服务控制台 也能快速检索全部事件。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VJd4354_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221212110238.png)


### 基于仪表盘配置告警

您可以通过以上预设的仪表盘配置告警，达到您所设置的条件则触发告警。操作详情如下：
1. 单击需要配置告警的仪表盘右侧的**快速添加告警**。
2. 在 **[日志服务控制台](https://console.cloud.tencent.com/cls/overview)**>**告警策略** 中新建告警策略。详情可参见 [配置告警策略](https://intl.cloud.tencent.com/document/product/614/39574)。


