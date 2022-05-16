<dx-alert infotype="alarm" title="温馨提示">
感谢您对腾讯云原生监控 TPS 的认可与信赖，为提供更优质的服务和更强大的产品能力，TPS 与原腾讯云 Prometheus 监控服务进行融合和升级，升级为 [TMP](https://intl.cloud.tencent.com/document/product/457/46734)。支持跨地域跨 VPC 监控，支持统一 Grafana 面板对接多监控实例实现统一查看。TMP 计费详情见 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156)，相关云资源使用详情见 [计费方式和资源使用](https://intl.cloud.tencent.com/document/product/457/46733)。若您只使用基础监控的 [免费指标](https://intl.cloud.tencent.com/document/product/457/46735)，TMP 不会收取任何指标费用。<br>
TPS 将于2022年5月16日下线，详情见 [公告](https://intl.cloud.tencent.com/document/product/457/46999)。TMP 已正式发布，欢迎 [了解试用](https://console.cloud.tencent.com/tke2/prometheus2)。TPS 已不支持创建新实例，我们提供一键 [迁移工具](https://intl.cloud.tencent.com/document/product/457/46736)，帮您一键将 TPS 实例迁移到 TMP，迁移前请 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737) 或降低采集频率，否则可能产生较高费用，再次感谢您对 TPS 的支持和信任。
</dx-alert>

## 操作场景
本文档介绍如何在云原生监控服务中配置告警规则。  

## 前提条件

在配置告警前，您需要完成以下准备工作：
- 已成功 [创建 Prometheus 监控实例](https://intl.cloud.tencent.com/document/product/457/46739)。
- 已将需要监控的集群关联到相应实例中，详情请参见 [关联集群](https://intl.cloud.tencent.com/document/product/457/38825)。
- 已将需要采集的信息添加到集群 [数据采集配置](https://intl.cloud.tencent.com/document/product/457/38826)。

## 操作步骤

### 配置告警规则

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要配置告警规则的实例名称，进入该实例详情页。
3. 在“告警配置”页面，单击**新建告警策略**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/55759e722ebf326889966a12f70a3e45.png)
4. 在“新建告警策略”页面，添加策略详细信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/5f053d31a0b7b60cd1154cac4297ba77.png)
 - **规则名称**：告警规则的名称，不超过40个字符。
 - **PromQL**：告警规则语句。
 - **持续时间**：满足上述语句所描述的条件的时间，达到该持续时间则会触发告警。
 - **Label**：对应每条规则添加 Prometheus 标签。
 - **告警内容**：告警触发后通过邮件或短信等渠道发送告警通知的具体内容。
 - **收敛时间**：在该周期内，若多次满足告警条件，仅会发送一次通知。
 - **生效时间**：一天之中可以发送告警通知的时间段。
 - **接收组**：接收告警信息的联系人组。
 - **告警渠道**：告警后发送告警内容的渠道。
6. 单击**完成**，即可完成新建告警策略。
>! 新建告警策略后，默认告警策略生效。

### 暂停告警
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要暂停告警的实例名称，进入该实例详情页。
3. 在“告警配置”页面，单击实例右侧的**更多** > **暂停告警**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/dd258e9e0694384fd12d01dda89b1fb2.png)
4. 在弹出的“关闭告警设置”窗口单击**确定**，即可暂停告警策略。

