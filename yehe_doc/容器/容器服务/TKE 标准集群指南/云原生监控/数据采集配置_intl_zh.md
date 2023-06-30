<dx-alert infotype="alarm" title="温馨提示">
感谢您对腾讯云原生监控 TPS 的认可与信赖，为提供更优质的服务和更强大的产品能力，TPS 与原腾讯云 Prometheus 监控服务进行融合和升级，升级为 [TMP](https://intl.cloud.tencent.com/document/product/457/46734)。支持跨地域跨 VPC 监控，支持统一 Grafana 面板对接多监控实例实现统一查看。TMP 计费详情见 [按量计费](https://intl.cloud.tencent.com/document/product/1116/43156)，相关云资源使用详情见 [计费方式和资源使用](https://intl.cloud.tencent.com/document/product/457/46733)。若您只使用基础监控的 [免费指标](https://intl.cloud.tencent.com/document/product/457/46735)，TMP 不会收取任何指标费用。<br>
TPS 将于2022年5月16日下线，详情见 [公告](https://intl.cloud.tencent.com/document/product/457/46999)。TMP 已正式发布，欢迎 [了解试用](https://console.cloud.tencent.com/tke2/prometheus2)。TPS 已不支持创建新实例，我们提供一键 [迁移工具](https://intl.cloud.tencent.com/document/product/457/46736)，帮您一键将 TPS 实例迁移到 TMP，迁移前请 [精简监控指标](https://intl.cloud.tencent.com/document/product/457/46737) 或降低采集频率，否则可能产生较高费用，再次感谢您对 TPS 的支持和信任。
</dx-alert>


## 操作场景

本文档介绍如何为已完成关联的集群配置监控采集项。

## 前提条件

在配置监控数据采集项前，您需要完成以下操作：
- 已成功 [创建 Prometheus 监控实例](https://intl.cloud.tencent.com/document/product/457/46739)。
- 已将需要监控的集群关联到相应实例中，详情请参见 [关联集群](https://intl.cloud.tencent.com/document/product/457/38825)。

## 操作步骤
### 配置数据采集

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要配置数据采集规则的实例名称，进入该实例详情页。
3. 在“关联集群”页面，单击实例右侧的**数据采集配置**，进入采集配置列表页。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/2f4a25e860c811521cd699d54210d9e9.png)
4. 在“数据采集配置”页中，新增数据采集配置。云原生监控预置了部分采集配置文件，用来采集常规的监控数据。您可以通过以下两种方式配置新的数据采集规则来监控您的业务数据。
<dx-tabs>
::: 通过控制台新增配置
#### 监控 Service 
1. 单击**新增**。
2. 在“新建采集配置”弹窗中，填写配置信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/90d6cb705291ec0507fc02cca712de8e.png)
 - **监控类型**：选择 “Service监控” 。
 - **名称**：填写规则名称。
 - **命名空间**：选择 Service 所在的命名空间。
 - **Service**：选择需要监控的 Service 名称。
 - **ServicePort**：选择相应的 Port 值。
 - **MetricsPath**：默认为 `/metrics`，您可根据需求执行填写采集接口。
 - **查看配置文件**：单击“配置文档”可查看当前配置文件。如果您有 relabel 等相关特殊配置的需求，可以在配置文件内进行编辑。
 - **探测采集目标**：单击**探测采集目标**，即可显示当前采集配置下能够采集到的所有 target 列表，您可通过此功能确认采集配置是否符合您的预期。

#### 监控工作负载
1. 单击**新增**。
2. 在“新建采集配置”弹窗中，填写配置信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c35d3c86973fbd742de817f026a2eab0.png)
 - **监控类型**：选择 “工作负载监控” 。
 - **名称**：填写规则名称。
 - **命名空间**：选择工作负载所在的命名空间。
 - **工作负载类型**：选择需要监控的工作负载类型。
 - **工作负载**：选择需要监控的工作负载。
 - **targetPort**：填写暴露采集指标的目标端口，通过端口找到采集目标。若端口填写错误将无法获取到正确的采集目标。
 - **MetricsPath**：默认为 `/metrics`，您可根据需求执行填写采集接口。
 - **查看配置文件**：单击“配置文档”可查看当前配置文件。如果您有 relabel 等相关特殊配置的需求，可以在配置文件内进行编辑。
 - **探测采集目标**：单击**探测采集目标**，即可显示当前采集配置下能够采集到的所有 target 列表，您可通过此功能确认采集配置是否符合您的预期。
:::
::: 通过\syaml\s文件新增配置
1. 单击**YAML新增**。
2. 在弹窗中，选择监控类型，并填写相应配置。本文以 “添加PodMonitors” 为例，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/a57bc9d2fd7227e88ee1d3a9b9f4ca66.png)
您可以按照社区的使用方式通过提交相应的 yaml 来完成数据采集的配置。
 - **工作负载监控**：对应配置为 PodMonitors。
 - **service 监控**：对应配置为 ServiceMonitors。
 - **RawJobs 监控**：对应配置为 RawJobs。
:::
</dx-tabs>
5. 单击**确认**完成配置。
6. 在该实例的“数据采集配置”页中，查看采集目标状态。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/6b483f8ea0d4a0538c761b473cedb9a8.png)
 **targets（1/1）**表示（实际抓取的 targets 数为1 / 探测的采集目标数为1）。当实际抓取数和探测数的数值相等时，显示为 up，即表示当前抓取正常。当实际抓取数小于探测数时，显示为 down，即表示有部分 endpoints 抓取失败。
单击字段值（1/1）即可查看采集目标的详细信息。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cca8ebe23797442415ff584b618ea6fc.png)
您还可以在该实例的“关联集群”页中，单击集群名称右侧的**更多** > **查看采集目标**，查看该集群下所有的采集目标情况。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/c536d75b4257741a85b4a28a3938e927.png)


















### 查看已有配置

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择右上角的**查看配置**。
3. 在弹出的“查看配置”窗口，查看 yaml 文件中当前配置的所有监控对象。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/e7a536ada035fa06b2661a18e46fe5ba.png)


### 查看采集目标

1. 登录 [容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**云原生监控**。
2. 在监控实例列表页，选择需要查看 Targets 的实例名称，进入该实例详情页。
3. 在“关联集群”页面，单击实例右侧的**查看采集目标**。
4. 在 Targets 列表页即可查看当前数据拉取状态。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/cca8ebe23797442415ff584b618ea6fc.png)

<dx-alert infotype="explain" title=" ">
<li>状态为“不健康”的 endpoints 默认显示在列表上方，方便及时查看。</li>
<li>实例中“采集目标”页面支持检索，可以按资源属性进行过滤。</li>
</dx-alert>




## 相关操作
### 挂载文件到采集器
在配置采集项的时候，如果您需要为配置提供一些文件，例如证书，可以通过以下方式向采集器挂载文件，文件的更新会实时同步到采集器内。

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
  prom-xxx 命名空间下的 configmap 添加如上 label，其中所有的 key 会被挂载到采集器的路径 `/etc/prometheus/configmaps/[configmap-name]/`。

- **prometheus.tke.tencent.cloud.com/scrape-mount = "true"**
 prom-xxx 命名空间下的 secret 添加如上 label，其中所有的 key 会被挂载到采集器的路径 `/etc/prometheus/secrets/[secret-name]/`。

