您可以更新运行中服务网格的配置，本文将介绍如何更新网格配置。

## 修改 Egress 流量模式

Egress 流量模式是配置网格内服务对外访问的放通策略，可选择 Registry Only（仅支持访问网格自动发现的服务与手动注册的服务）或 Allow Any（可访问任何地址）。

以下是配置网格 Egress 流量模式的步骤：
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。
![](https://qcloudimg.tencent-cloud.cn/raw/bd10b1c574235a8ac2226222b812ee9f.png)

2. 在网格基本信息页面单击 Egress 流量模式栏的编辑按钮，进入**调整 Egress 流量模式**弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/7c97e45ea182ae955c2e10b5871590f2.png)

3. 按照需要选择 **Allow Any** 或 **Registry Only**，单击**保存**更新 Egress 流量模式。
![](https://qcloudimg.tencent-cloud.cn/raw/efc5846fe97bc698b75945a9a778c870.png)


## 启用 HTTP1.0 支持

Istio 默认不支持 HTTP 1.0，如有需要，可以在网格基本信息中开启：

![](https://staticintl.cloudcachetci.com/yehe/backend-news/cYMA448_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111163424.png)

## 关闭 HTTP 自动重试

对于失败的 HTTP 请求，Istio 默认会重试2次，某些情况下这不符合您的预期，可以在网格基本信息页里关闭自动重试：

![](https://staticintl.cloudcachetci.com/yehe/backend-news/AcMB792_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111163839.png)

关闭对全网格生效，但您仍然可以对特定的 Virtual Service 显式设定重试策略。

## 启用 DNS 代理

istio 的 Sidecar 支持 DNS 代理，启用后，DNS 的流量也会被拦截，由 Sidecar 直接响应 DNS 请求，一方面 sidecar 会有 DNS 缓存，可以加速 DNS 响应，另一方面，多集群网格的场景，跨集群访问 service 时，不需要在 client 所在集群创建同名 service 也能正常解析 service。您可以参考以下步骤开启 DNS 转发。
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。

2. 在基本信息页面，单击 **DNS Proxying > DNS 转发**右侧的![](https://qcloudimg.tencent-cloud.cn/image/document/5d77e87a83754f081a5e4be6a8612316.png)，开启 DNS 转发。如下图所示：
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/Fx2T315_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111164108.png)

   如果您需要为没有定义 addresses 的 ServiceEntry 自动分配 IP，可以开启**自动 IP 分配**。更多内容可参考 [Address auto allocation](https://istio.io/latest/docs/ops/configuration/traffic-management/dns-proxy/#address-auto-allocation)。
