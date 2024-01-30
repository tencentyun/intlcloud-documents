本文将为刚入门 Elasticsearch Service（ES）的用户提供一条学习的路径。

## 1. 熟悉 ES 的基础知识
- [为什么选择腾讯云 ES？](https://intl.cloud.tencent.com/document/product/845/16479)
- [ES 有什么功能？](https://intl.cloud.tencent.com/document/product/845/16780)
- [ES 的产品性能。](https://intl.cloud.tencent.com/document/product/845/40975)
- [ES 的各个应用场景介绍。](https://intl.cloud.tencent.com/document/product/845/16480)
- [ES 的高级特性（X-Pack）介绍。](https://intl.cloud.tencent.com/document/product/845/30943)
- [ES 能力与限制说明。](https://intl.cloud.tencent.com/document/product/845/16481)



## 2. ES 的计费模式
腾讯云 ES 的计费模式为按量计费。计费详情请参见 [计费说明](https://intl.cloud.tencent.com/document/product/845/18379)。



## 3. 新手入门
**3.1 集群规格和容量配置评估**
在购买集群前，需要根据实际情况对具体的业务进行评估，以确保创建的集群是符合您实际需求的。详情请参见 [集群规格和容量配置评估](https://intl.cloud.tencent.com/document/product/845/19551)。
**3.2 选购 ES 集群**
在使用腾讯云 ES 前，您需要注册腾讯云账号，然后在 [购买页](https://intl.cloud.tencent.com/product/es) 单击【立即选购】创建集群，详情可参考 [创建集群](https://intl.cloud.tencent.com/document/product/845/19536)。
**3.3 访问集群**
集群创建成功后，即可开始访问集群，启用 [ES 集群用户登录认证](https://intl.cloud.tencent.com/document/product/845/35275) 可以提升集群访问的安全性。访问集群有三种方式：[通过 API 访问集群](https://intl.cloud.tencent.com/document/product/845/19540)、[通过客户端访问集群](https://intl.cloud.tencent.com/document/product/845/19538)、[通过 Kibana 访问集群](https://intl.cloud.tencent.com/document/product/845/19541)。


## 4. 控制台功能概述

| 如果您想 | 	您可以阅读 |
|---------|---------|
| 在集群列表中查看集群的状态信息 | [集群状态](https://intl.cloud.tencent.com/document/product/845/16996) |
| 重启集群，可根据集群的情况使用此功能对集群进行重启  | [重启集群](https://intl.cloud.tencent.com/document/product/845/32597) |
| 销毁集群      |     [销毁集群](https://intl.cloud.tencent.com/document/product/845/30949)       |
| 创建支持多可用区的集群    |       [集群多可用区部署](https://intl.cloud.tencent.com/document/product/845/32591)     |
| 了解集群变配的概念和原理，扩缩容集群    | [调整配置](https://intl.cloud.tencent.com/document/product/845/30944) 和 [集群变配建议和原理介绍](https://intl.cloud.tencent.com/document/product/845/35713)  |
| 在集群中配置同义词和 YML       |   [同义词配置](https://intl.cloud.tencent.com/document/product/845/36418) 和 [YML 配置](https://intl.cloud.tencent.com/document/product/845/37438)         |
| 在集群中配置插件     |  [插件列表](https://intl.cloud.tencent.com/document/product/845/37440)、[IK 分词插件](https://intl.cloud.tencent.com/document/product/845/37441) 和 [QQ 分词插件](https://intl.cloud.tencent.com/document/product/845/36776)        |
| 监测运行中的集群的运行情况      |        [查看监控](https://intl.cloud.tencent.com/document/product/845/30947)、[配置告警](https://intl.cloud.tencent.com/document/product/845/30948) 和 [监控告警配置建议](https://intl.cloud.tencent.com/document/product/845/32608)    |
| 查询集群日志  | [查询集群日志](https://intl.cloud.tencent.com/document/product/845/30950)   |
| 备份数据  | [自动快照备份](https://intl.cloud.tencent.com/document/product/845/32587)、[使用 COS 进行备份及恢复](https://intl.cloud.tencent.com/document/product/845/19549)  |
| 升级集群版本和高级特性     |      [升级 ES 集群](https://intl.cloud.tencent.com/document/product/845/32600) 和 [ES 版本升级检查](https://intl.cloud.tencent.com/document/product/845/32599) |


## 5. 最佳实践
### 5.1 数据迁移和同步
**1. 数据迁移**
数据如果要迁移至腾讯云 ES，您可以根据自己的业务需要选择合适的迁移方案。数据迁移方式：COS 快照、logstash、elasticsearch-dump，详情可参考 [数据迁移](https://intl.cloud.tencent.com/document/product/845/32614)。
**2. 数据接入 ES**
通过组件 logstash 和 beats，介绍不同类型的数据源接入 ES 的方式，详情可参考 [数据接入 ES](https://intl.cloud.tencent.com/document/product/845/17343)。
**3. MySQL 数据实时同步到 ES**
以同步 mysql binlog 的方式实时同步数据到 ES，详情请参考 [MySQL 数据实时同步到 ES](https://intl.cloud.tencent.com/document/product/845/32576)。

### 5.2 应用场景构建
**1. 构建日志分析系统**
以最典型的日志分析架构 Filebeat + Elasticsearch + Kibana 和 Logstash + Elasticsearch + Kibana 为例，介绍如何将用户的日志导入到 ES，并可以在浏览器访问 Kibana 控制台进行查询与分析。详情可查阅 [构建日志分析系统](https://intl.cloud.tencent.com/document/product/845/32590)。

### 5.3 索引设置
**1. 默认索引模板说明和调整**
对索引模板进行说明及调整，详情请参考 [默认索引模板说明和调整](https://intl.cloud.tencent.com/document/product/845/32607)。
**2. 使用 Curator 管理索引**
通过 Curator 管理索引，以清理创建时间超过7天的索引、每天定时备份指定的索引、定时将索引从热节点迁移至冷节点等，详情请参考 [使用 Curator 管理索引](https://intl.cloud.tencent.com/document/product/845/32613)。
**3. 冷热分离与索引生命周期管理**
根据业务需要指定冷热节点规格，快速建立一个冷热分离架构的 ES 集群，详情请参考 [冷热分离与索引生命周期管理](https://intl.cloud.tencent.com/document/product/845/34890)。

### 5.4 SQL 支持
腾讯云 Elasticsearch 支持使用 SQL 代替 DSL 查询语言，对于从事产品运营、数据分析等工作以及初次接触 ES 的人，使用 SQL 语言进行查询，将会降低他们使用 ES 的学习成本。详情请参考 [SQL 支持](https://intl.cloud.tencent.com/document/product/845/32574)。


## 6. 新手常见问题
### 6.1 产品相关问题
- [ES 适用于哪些业务场景？](https://intl.cloud.tencent.com/document/product/845/16599)
- [有未支付的转换订单，升级了集群的配置，转换订单还有效吗？](https://intl.cloud.tencent.com/document/product/845/16599)
- [在成功购买后，是否支持更换云硬盘的类型？](https://intl.cloud.tencent.com/document/product/845/16599)

### 6.2 集群异常问题 
- [集群健康状态异常（RED、YELLOW）如何解决？](https://intl.cloud.tencent.com/document/product/845/40983)
- [常用清理内存的方法是什么？](https://intl.cloud.tencent.com/document/product/845/40982)
- [写入拒绝或查询拒绝问题如何解决？](https://intl.cloud.tencent.com/document/product/845/40981)
- [集群整体 CPU 使用率过高问题如何解决？](https://intl.cloud.tencent.com/document/product/845/40980)
- [ 集群磁盘使用率高和 read_only 状态问题如何解决？](https://intl.cloud.tencent.com/document/product/845/40979)
- [集群负载不均的问题如何解决？](https://intl.cloud.tencent.com/document/product/845/40978)



## 7. 反馈与建议
使用腾讯云 ES 产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。
