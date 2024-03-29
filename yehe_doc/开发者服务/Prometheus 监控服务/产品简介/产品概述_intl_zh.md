Prometheus 监控服务（Managed Service for Prometheus TMP）在继承开源 Prometheus 监控能力的同时 ，还提供高可用的 Prometheus 服务、开源可视化的 Grafana和云监控告警，为您减少用户的开发及运维成本。

## 开源 Prometheus 简介

Prometheus 是一个开源监控系统。与 Kubernetes 相似，Prometheus 受启发于 Google 的 Borgman 监控系统，而 Kubernetes 也是从 Google 的 Borg 演变而来的。Prometheus 始于2012年，并由 SoundCloud 内部工程师开发，于2015年1月发布。2016年5月，其成为继 Kubernetes 之后第二个正式加入 [Cloud Native Computing Foundation（CNCF）](https://www.cncf.io/) 基金会的项目。现最常见的 Kubernetes 容器管理系统中，通常会搭配 Prometheus 进行监控。


Prometheus 具有如下特性：
- 自定义多维数据模型（时序列数据由 Metric 和一组 Key/Value Label 组成）。
- 灵活而强大的查询语言 PromQL，可利用多维数据完成复杂的监控查询。
- 不依赖分布式存储，支持单主节点工作。
- 通过基于 HTTP 的 Pull 方式采集时序数据。
- 可通过 PushGateway 的方式来实现数据 Push 模式。
- 可通过动态的服务发现或者静态配置去获取要采集的目标服务器。
- 结合 Grafana 可方便的支持多种可视化图表及仪表盘。

## 产品功能

根据监控分层，Prometheus 监控服务覆盖了业务监控、应用层监控、中间件监控、系统层监控，结合云监控告警和开源 Grafana 可以提供一站式全方位的监控体系，帮助业务快速发现和定位问题，减轻故障给业务带来的影响。
- 系统层监控：例如 CPU、Memory、Disk 和 Network 等。
- 中间组件层监控：例如 Kafka、MySQL 和 Redis 等。
- 应用层监控：应用服务监控，例如 JVM、HTTP 和 RPC 等。
- 业务监控：业务黄金指标，例如登录数和订单量等。

## 产品优势
与开源的 Prometheus 对比，Prometheus 监控服务优势如下：
![](https://qcloudimg.tencent-cloud.cn/raw/dee21237fe9f010a39d99e7afb2a3e46.png)

- 更轻量、更稳定、可用性更高。
- 完全兼容开源 Prometheus 生态。
- 无需您手动搭建，节省开发成本。
- 与腾讯云容器服务高度集成，节省与 Kubernetes 集成的开发成本。
- 与云监控告警体系打通，节省开发告警通知成本。
- 同时也集成了常用的 Grafana Dashboard 及告警规则模板。



