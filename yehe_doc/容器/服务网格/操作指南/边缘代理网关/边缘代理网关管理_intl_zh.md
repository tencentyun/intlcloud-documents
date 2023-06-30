边缘代理网关是负责网格出口与入口流量负载均衡的特殊数据面，它不以 Sidecar 的形式，而是以独立 Pod 的形式部署在您的集群内，分为 Ingress Gateway 和 Egress Gateway 两种类型。其中，一个 Ingress Gateway 实例包含数据面的 Envoy Pod 和它关联的负载均衡 CLB 实例（公网或内网），TCM 提供托管的 [边缘代理网关控制器](#gatewayController)，已经实现了 Ingress Gateway 配置与 CLB 的自动化集成，您可以通过 Istio CRD 配置 Ingress Gateway，相关设置 TCM 会自动同步至关联的 CLB 实例，同步的配置包括端口配置和增强功能的端口监听规则配置两部分。即 Envoy 容器和关联的 CLB 作为一个整体，为您提供入口边缘代理网关的能力。

如您需要网格出入口流量负载均衡的能力，您需先要创建 Ingress Gateway 或 Egress Gateway 实例，再通过 Gateway，VirtualService，DestinationRule 等 Istio CRD 配置边缘代理网关的监听规则和流量管理（路由）规则。监听规则通过 Gateway CRD 配置，流量管理规则通过 VirtualService、Destination Rule 配置（与东西向流量管理语法一致）。下图是边缘代理网关实例与 Istio CRD 配置的关系示意图。

![](https://qcloudimg.tencent-cloud.cn/raw/4ff31308ce78b47e93a0bdc8f0a4ab39.png)

## 创建边缘代理网关

1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)。
2. 您可以在网格创建页面，添加服务发现集群后，创建边缘代理网关。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/fd517f22c2aea129e9662128f2ff20c7.png)
或在网格详情页面边缘代理网关 Tab 单击**新建**创建边缘代理网关。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0b8fea6b80a0b153fc5f8530f4c916c2.png)

创建边缘代理网关重要配置项说明：

| 配置项 | 描述 |
| ----- | ----- |
| 类型 | 选择创建 Ingress 网关或 Egress 网关。|
| 接入集群 | 选择网关创建的 Kubernetes 集群。 |
| namespace | 选择网关创建的命名空间。 |
| 访问类型 | Ingress Gateway 参数。选择 CLB 的访问类型，支持公网和内网。 |
| 负载均衡器 | Ingress Gateway 参数。选择自动创建负载均衡器，或选择复用现有负载均衡器，复用已有负载均衡器更多介绍参见 [Service 使用已有 CLB](https://intl.cloud.tencent.com/document/product/457/36835)。 |
| 计费模式 | Ingress Gateway 参数。选择 CLB 的计费模式，支持按流量计费或按带宽计费，更多关于 CLB 计费的信息，参见 [CLB 计费概述](https://intl.cloud.tencent.com/document/product/214/36999) 。|
| 带宽上限 | Ingress Gateway 参数。选择 CLB 的带宽上限，0 - 2048 Mbps。 |
| CLB 直连 Pod | Ingress Gateway 参数。例如，网关接入集群网络模式为 VPC-CNI，即可开启 CLB 直连 Pod，将不再进行 NodePort 转发，具有更高性能，支持保留客户端源 IP、Pod 层级会话保持与健康检查，更多详情请参见 [使用 LoadBalancer 直连 Pod 模式 Service](https://intl.cloud.tencent.com/document/product/457/36837)。 |
| 保留客户端源 IP | Ingress Gateway 参数。设置网关 Service 的 ExternalTrafficPolicy 为 Local，源 IP 保留，并开启 Local 绑定与 Local 加权平衡。开启 CLB 直连 Pod 时，该参数失效。更多详情请参见 [Service 后端选择](https://intl.cloud.tencent.com/document/product/457/36836)。 |
| 组件配置 | 配置网关的 CPU 和 内存资源，以及 HPA 伸缩策略。 |

## 边缘代理部署模式

边缘代理网关有**普通模式**，**专有模式**两种部署形态，其中：
- **普通模式**：网关服务部署在所选的业务集群中，与其他业务Pod无差别部署。
- **专有模式**：某些场景下为了提升服务的稳定性，您需要将边缘代理网关部署在专有节点上。专有模式需要先选择将部分集群节点添加到专有资源池中，网格将会为选中的节点设置污点以保证独享。设置后所有 Ingress/Egress Gateway 都将仅部署在选中的节点中。您还可以在高级设置中为特定的 Gateway 进一步指定节点。

您可以在网格创建页、或组件管理页重新调整网关部署模式：
>? 调整部署模式会触发网关服务调度，可能会对业务流量产生影响。
>
![](https://qcloudimg.tencent-cloud.cn/raw/95242718623ea1eafbfbdbf5ce2f8f61.png)


## 更新边缘代理网关配置

边缘代理网关创建后，您可以修改边缘代理网关的关联 CLB 带宽（仅 Ingress Gateway）、实例数量、HPA 伸缩策略及资源定义配置。

### 修改 CLB 带宽

您可以修改 Ingress Gateway 关联的 CLB 实例的带宽。在对应网格详情页面的**基本信息** Tab 边缘代理网关部分可以编辑 Ingress Gateway 绑定的 CLB 配置。
![](https://qcloudimg.tencent-cloud.cn/raw/ae3d478889654c9db7beac6cefca47e0.png)


### 修改组件实例数量

在**网格详情 > 组件管理**可以调整组件的实例数量。

![](https://qcloudimg.tencent-cloud.cn/raw/4432668506a10c90d0e0edf1a45778b9.png)

### 修改组件 HPA 伸缩策略

在**网格详情 > 组件管理**可以编辑组件的 HPA 策略。支持按照 CPU、内存、网络、硬盘指标配置伸缩策略。如下图所示：

![](https://qcloudimg.tencent-cloud.cn/raw/3a84abdd67d3b7ff92d81173ab29a88c.png)

### 修改组件资源定义

在**网格详情 > 组件管理**可以编辑组件的资源定义，包括 CPU、内存的 request 和 limit 值。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/40dbc9fec706d2f2f33d3729105f0861.png)

## 删除边缘代理网关

您可以在网格详情-组件管理-边缘代理网关删除指定边缘代理网关。步骤如下：

1. 进入网格详情页，单击**组件管理**，选择**边缘代理网关**，在需要删除的网关对应行**操作**列单击**更多** > **删除**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0ede45c26792ea8c88d8e4b12a3fb188.png)
2. 在**删除边缘代理网关**弹窗，确认删除的网关名称，单击**确定**完成删除。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ba2d32f4b8ad0c5ea97fd7ad02c42834.png)

## TCM 边缘代理网关控制器实现自动对接 CLB [](id:gatewayController)

TCM 实现了托管的边缘代理网关控制器，该控制器会实时监测下发到 Ingress Gateway 的 Gateway 配置，解析当前的端口配置，同步当前端口配置到 CLB，您无需再手动配置 CLB 端口。CLB 端口与 Ingress Gateway Service 端口、Ingress Gateway 容器端口的映射关系是一一映射，即如果在 Gateway CRD 中定义 `80` 端口，TCM 边缘代理网关控制器会配置 Ingress Gateway 实例的容器端口为 `80`，服务端口为 `80`，以及同步开启关联 CLB 的 `80` 端口。

TCM 边缘代理网关控制器还实现了 SSL 证书解包上移至 CLB 的功能，实现在 CLB 做证书解包后，Ingress Gateway 再提供流量管理的能力。在 Gateway 中配置证书上移后，边缘代理网关控制器会解析配置上移的端口、域名、证书，并将配置同步至 Ingress Gateway 绑定的 CLB 实例。

![](https://qcloudimg.tencent-cloud.cn/raw/3726322a202d61f002c6e102ca5b0d54.png)
