<dx-alert infotype="alarm" title="温馨提示">
感谢您对腾讯云原生监控 TPS 的认可与信赖，为提供更优质的服务和更强大的产品能力，TPS 与原腾讯云 Prometheus 监控服务进行融合和升级，升级为 [TMP](https://intl.cloud.tencent.com/document/product/457/46734)。支持跨地域跨 VPC 监控，支持统一 Grafana 面板对接多监控实例实现统一查看。TMP 计费详情见 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156)，相关云资源使用详情见 [计费方式和资源使用](https://intl.cloud.tencent.com/document/product/457/46733)。若您只使用基础监控的 [免费指标](https://intl.cloud.tencent.com/document/product/457/46735)，TMP 不会收取任何指标费用。<br>
TPS 即将下线。TMP 已正式发布，欢迎 [了解试用](https://console.cloud.tencent.com/tke2/prometheus2)。TPS 已不支持创建新实例，我们提供一键 [迁移工具](https://intl.cloud.tencent.com/document/product/457/46736)，帮您一键将 TPS 实例迁移到 TMP，迁移前请 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737) 或降低采集频率，否则可能产生较高费用，再次感谢您对 TPS 的支持和信任。
</dx-alert>

TPS 支持一键迁移到 TMP。您可以迁移单独的实例，也可以批量迁移单地域下的实例。每个 TPS 实例的迁移时间一般在十分钟左右。**新的 TMP 实例将以 “旧实例名 (trans-from-prom-xxx)”命名，其中“旧实例名”为原 TPS 的实例名，“xxx” 为原 TPS 实例 ID。**迁移之后，您可以在新的 TMP 实例查看新的监控数据，也可以在旧的实例中查看以前的监控数据，需注意，旧实例将在服务停止时删除。




迁移步骤如下：
<dx-steps>
-迁移 Grafana 配置
-创建 Grafana 实例
-创建 TMP 实例
-TMP 绑定 TPS 之前关联的集群
-迁移采集配置
-迁移告警策略
-迁移聚合规则
</dx-steps>

## 迁移注意事项

如果您有相关的程序平台或系统依赖 TPS 的 **Prometheus 数据查询地址和 Grafana 地址**。迁移后请及时更换为 TMP 里面相应的地址。否则旧的 TPS 实例在服务停止删除后，您的 **Prometheus 数据查询地址和 Grafana 地址** 将失效。

#### （旧）TPS Prometheus 数据查询地址和 Grafana 地址 
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的 **[云原生监控](https://console.cloud.tencent.com/tke2/prometheus)**。
2. 单击实例 ID ，进入实例的“基本信息”页，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/b5b9fc3ef9f9e60c952433dba3bbc7ba.png)

#### （新）TMP Prometheus 数据查询地址和 Grafana 地址 
1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的 **[Prometheus 监控](https://console.cloud.tencent.com/tke2/prometheus2)**。
2. 单击实例 ID ，进入实例的“基本信息”页，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/90393196785809a05e85dcb5ac172b24.png)

>? 迁移完成后，请勿在旧的 TPS 实例里面关联新的集群或采集规则，这部分新增的改变将不会自动同步到新的 TMP 实例中。

## 操作步骤

### 单实例迁移

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的 **[云原生监控](https://console.cloud.tencent.com/tke2/prometheus)**。
2. 在当前的云原生监控的实例列表页，在上方选择需要迁移的实例所在的地域。
3. 单击实例右方的**一键迁移**。
4. 在弹窗中，选择新的 TMP 实例需要的**网络**和**数据存储时间**。
	- 网络：新的 TMP 实例的 VPC 和子网默认和原来的 TPS 实例一样。若您要选择其它 VPC，请注意该 VPC 首先需要和监控的集群所在的 VPC 网络已打通。
	- 数据存储时间：默认15天。
>! 请查看 TMP 涉及 [计费方式](https://intl.cloud.tencent.com/document/product/1116/43156) 和相关 [云资源使用情况](https://intl.cloud.tencent.com/document/product/457/46733)。若费用过高，建议您 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737)。
>
5. 单击**确定**。当 TPS 实例状态的括号中内容显示“已迁移”，表示迁移成功。
6. TPS 迁移完成后，您可以在 **[Prometheus 监控](https://console.cloud.tencent.com/tke2/prometheus)** 控制台，在同样的地域里找到一个名为**“旧实例名 (trans-from-prom-xxx)” 的 TMP 新实例，其中“旧实例名”为原 TPS 的实例名，“xxx” 为原 TPS 实例 ID。**
>? 迁移完成后，请勿在旧的 TPS 实例里面关联新的集群或采集规则，这部分新增的改变将不会自动同步到新的 TMP 实例中。

### 实例批量迁移

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的 **[云原生监控](https://console.cloud.tencent.com/tke2/prometheus)**。
2. 在当前的云原生监控的实例列表页，在上方选择需要迁移的实例所在的地域。
3. 勾选状态为“未迁移”的实例，单击上方的“一键迁移”。
>! 
>- 批量迁移不支持择新 TMP 实例的 VPC 和子网，如您有类似需求，请进行**单实例迁移**。
>! 请查看 TMP 涉及 [计费方式](https://intl.cloud.tencent.com/document/product/1116/43156) 和相关 [云资源使用情况](https://intl.cloud.tencent.com/document/product/457/46733)。若费用过高，建议您 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737)。
4. 单击**确定**。当 TPS 实例状态的括号中内容显示“已迁移”，表示迁移成功。
5. TPS 迁移完成后，您可以在 **[Prometheus 监控](https://console.cloud.tencent.com/tke2/prometheus)** 的控制台，在同样的地域里找到一个名为**“旧实例名 (trans-from-prom-xxx)”的 TMP 新实例，其中“旧实例名”为原 TPS 的实例名，“xxx” 为原 TPS 实例 ID。**
>? 迁移完成后，请勿在旧的 TPS 实例里面关联新的集群或采集规则，这部分新增的改变将不会自动同步到新的 TMP 实例中。
