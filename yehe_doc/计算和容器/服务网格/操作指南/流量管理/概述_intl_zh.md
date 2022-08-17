## TCM 流量管理模型

TCM 完全兼容 Istio 管理流量的原生 CRD：Gateway，VirtualService 和 DestinationRule，并对原生流量管理语法做了产品化呈现，下图是 TCM 的流量管理模型：

![](https://qcloudimg.tencent-cloud.cn/raw/629939a71bc86e64f73df1d5036a3f41.png)

TCM 使用 Gateway，VirtualService 和 DestinationRule 管理流量。

- Gateway：定义网关的端口、监听规则、证书配置，网关与 Gateway 配置是一对多的关系，Gateway 通过 selector 字段指定配置下发的边缘代理网关。
- VirtualService：定义指定 Host 的路由规则和流量操作规则，VirtualService 通过 hosts 字段指定绑定的域名。可规定流量来源是边缘代理网关或 mesh 内部。
- DestinationRule：定义服务的版本和流量策略，包括负载均衡、健康检查、连接池等流量策略。服务与 DestinationRule 是一对一的绑定关系。

## 流量管理配置方式

当前 TCM 提供以下两种方式配置 Gateway，VirtualService 和 DestinationRule：


<dx-tabs>
::: 控制台 UI 配置
您可以通过控制台 UI 创建，删除，更新，查看 Gateway，VirtualService，DestinationRule。

- 创建 Gateway：
![](https://qcloudimg.tencent-cloud.cn/raw/425f12e06765f2e912e85234692a7042.png)
- 创建 VirtualService：
![](https://qcloudimg.tencent-cloud.cn/raw/a244f690e1d666f871d6d9531caa2129.png)
- 创建 DestinationRule：DestinationRule 与服务是一对一绑定关系，创建与管理在服务详情页面：
![](https://qcloudimg.tencent-cloud.cn/raw/4c51598a9c2d3162dab10e6e85be0c43.png)
![](https://qcloudimg.tencent-cloud.cn/raw/c902d405dbf4cce7fe146f5efad2e2a5.png)
:::
::: YAML 创建资源
您可以通过网格管理界面右上角的**YAML 创建资源**创建 Istio 资源或 Kubernetes 资源。如您提交的 YAML 中含有 Kubernetes 资源，且当前网格管理了多个集群时，您需要选择 YAML 资源提交的目的集群。

![](https://qcloudimg.tencent-cloud.cn/raw/507b0c8c8d8888a877788744f66a4819.png)
:::
</dx-tabs>

