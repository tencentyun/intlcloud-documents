<dx-alert infotype="alarm" title="温馨提示">
感谢您对腾讯云原生监控 TPS 的认可与信赖，为提供更优质的服务和更强大的产品能力，TPS 与原腾讯云 Prometheus 监控服务进行融合和升级，升级为 [TMP](https://intl.cloud.tencent.com/document/product/457/46734)。支持跨地域跨 VPC 监控，支持统一 Grafana 面板对接多监控实例实现统一查看。TMP 计费详情见 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156)，相关云资源使用详情见 [计费方式和资源使用](https://intl.cloud.tencent.com/document/product/457/46733)。若您只使用基础监控的 [免费指标](https://intl.cloud.tencent.com/document/product/457/46735)，TMP 不会收取任何指标费用。<br>
TPS 即将下线。TMP 已正式发布，欢迎 [了解试用](https://console.cloud.tencent.com/tke2/prometheus2)。TPS 已不支持创建新实例，我们提供一键 [迁移工具](https://intl.cloud.tencent.com/document/product/457/46736)，帮您一键将 TPS 实例迁移到 TMP，迁移前请 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737) 或降低采集频率，否则可能产生较高费用，再次感谢您对 TPS 的支持和信任。
</dx-alert>

## 操作场景

本文档介绍应对复杂查询场景时如何配置聚合规则，提高查询的效率。

## 前提条件

在配置聚合规则前，您需要完成以下操作：
- 已登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，并创建独立集群。
- 已在集群所在 VPC 中 [创建监控实例](https://intl.cloud.tencent.com/document/product/457/46739)。

## 操作步骤

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要创建聚合规则的实例名称，进入该实例详情页。
3. 在“聚合规则”页面，单击**新建聚合规则**。
4. 在弹出的“新增聚合规则”窗口，编辑聚合规则。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/07bf41b601845cb1ea9705a6ae16c881.png)
6. 单击**确定**，即可完成创建聚合规则。
