网格（mesh）实例，是管理服务的逻辑隔离空间，同一网格内的服务之间可通信。
![](https://qcloudimg.tencent-cloud.cn/raw/0839f6b1448c611cc18ee547b8b2367a.png)

以下是网格生命周期状态说明：

 

<table>
<thead>
  <tr>
    <th width="20%">状态</th>
    <th>说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>创建中</td>
    <td>网格创建过程中，网格详情无法查看。</td>
  </tr>
  <tr>
    <td>运行中</td>
    <td>网格正常运行状态。</td>
  </tr>
  <tr>
    <td>升级中</td>
    <td>网格正在进行版本升级，部分功能无法使用。</td>
  </tr>
  <tr>
    <td>闲置</td>
    <td>当网格管理的服务发现集群被删除或解关联后，将进入闲置状态（idle），闲置状态的网格可正常查看，但由于没有业务实体，部分功能将不可用。您可以为网格重新添加服务发现集群使其恢复正常状态。</td>
  </tr>
  <tr>
    <td>无效</td>
    <td>当网格处于闲置状态超过 30 天后，或独立网格主集群被删除，网格将进入无效状态，您将不再能对网格进行删除之外的其他操作。</td>
  </tr>
  <tr>
    <td>异常</td>
    <td>网格中部分组件异常导致功能网格功能已经受到影响。</td>
  </tr>
</tbody>
</table>

网格创建过程中需要进行以下几部分配置：
- **添加服务发现集群**
通过添加服务发现的 Kubernetes 集群自动发现集群内的服务实现，也可通过手动注册服务实现。网格中已发现的服务将出现在**服务网格控制台  > 网格详情 > 服务**列表页中。服务被发现后，可以被网格中其他服务访问。详细指引请查看 [服务发现管理](https://intl.cloud.tencent.com/document/product/1152/47467)。
- **创建边缘代理网关**
边缘代理网关分为 Ingress 和 Egress 两种类型，是网格流量的出入口，其中 Ingress 类型的边缘代理网关必须创建，流量才能进入网格，Egress 类型边缘代理网关可选创建，详细指引请查看 [边缘代理网关管理](https://intl.cloud.tencent.com/document/product/1152/47471)。
- **为服务注入 Sidecar**
Sidecar 容器承担数据面流量管理、规则生效、监控上报等网格治理工作，是网格流量治理和观测的基础，因此对于需要进行流量管理和观测的服务，需要为其注入 Sidecar，详细指引请查看 [网格配置](https://intl.cloud.tencent.com/document/product/1152/47464)。
- **可观测性后端服务配置**
可观测性分为监控指标查看、链路追踪、日志管理三部分。服务网格支持与腾讯云 Prometheus 监控 TMP 、应用性能观测 APM、日志服务 CLS 集成，提供更丰富、一体化的可观测能力，同时服务网格也支持对接第三方 Prometheus、Jaeger/Zpkin 服务，为用户提供更大的组件扩展性。详细指引请查看 [可观测性](https://intl.cloud.tencent.com/document/product/1152/47478)。

网格创建后，对网格进行流量规则调度，可以通过控制台或提交 YAML 文件配置的形式为网格创建流量治理规则，当前 TCM 完全兼容 Istio 原生语法，详细指引请查看 [流量管理](https://intl.cloud.tencent.com/document/product/1152/47474)。
