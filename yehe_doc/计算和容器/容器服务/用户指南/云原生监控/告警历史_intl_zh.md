<dx-alert infotype="alarm" title="温馨提示">
感谢您对腾讯云原生监控 TPS 的认可与信赖，为提供更优质的服务和更强大的产品能力，TPS 与原腾讯云 Prometheus 监控服务进行融合和升级，升级为 [TMP](https://intl.cloud.tencent.com/document/product/457/46734)。支持跨地域跨 VPC 监控，支持统一 Grafana 面板对接多监控实例实现统一查看。TMP 计费详情见 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156)，相关云资源使用详情见 [计费方式和资源使用](https://intl.cloud.tencent.com/document/product/457/46733)。若您只使用基础监控的 [免费指标](https://intl.cloud.tencent.com/document/product/457/46735)，TMP 不会收取任何指标费用。<br>
TPS 将于2022年5月16日下线，详情见 [公告](https://intl.cloud.tencent.com/document/product/457/46999)。TMP 已正式发布，欢迎 [了解试用](https://console.cloud.tencent.com/tke2/prometheus2)。TPS 已不支持创建新实例，我们提供一键 [迁移工具](https://intl.cloud.tencent.com/document/product/457/46736)，帮您一键将 TPS 实例迁移到 TMP，迁移前请 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737) 或降低采集频率，否则可能产生较高费用，再次感谢您对 TPS 的支持和信任。
</dx-alert>

## 操作场景

本文档介绍如何在云原生监控功能服务中查看告警历史。

## 前提条件

在查看告警历史前，需要完成以下前置操作：
- 已成功 [创建 Prometheus 监控实例](https://intl.cloud.tencent.com/document/product/457/46739)。
- 已将需要监控的集群关联到相应实例中，详情请参见 [关联集群](https://intl.cloud.tencent.com/document/product/457/38825)。
- 已将需要采集的信息添加到集群 [数据采集配置](https://intl.cloud.tencent.com/document/product/457/38826)。
- 已 [配置告警规则](https://intl.cloud.tencent.com/document/product/457/38828)。

## 操作步骤


1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要查看告警历史的实例名称，进入该实例详情页。
3. 在“告警历史”页面，选择时间即可查看告警历史。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1c00ed84dd12db38b5d7b23b8a0c9d72.png)
