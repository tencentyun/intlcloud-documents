## 配置 Sidecar 自动注入

TCM 当前支持在控制台为指定的 Namespace 开启 Sidecar 自动注入，开启后该 Namespace 下新创建的 workload 将会自动安装网格 Sidecar，由于注入是在 workload 创建过程中完成的，因此开启注入无法为已存在的 workload 自动安装 Sidecar，您可以通过重建 workload 完成 Sidecar 自动注入。

以下是配置 Namespaces 级 Sidecar 自动注入的步骤：
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。
![](https://qcloudimg.tencent-cloud.cn/raw/5bfd233ffe3448492283e1dce1f73bc8.png)

2. 在服务列表页点击单击**Sidecar 自动注入**，进入 **Sidecar 自动注入配置**弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/aae8187f5a5e5d6170c4d427adb8dac1.png)

3. 按需勾选需要 **Sidecar** 自动注入的 **namespace**，单击**确定**完成 Sidecar 自动注入配置。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ETQY297_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111164850.png)


## 自定义 Sidecar 注入

TCM 也支持您通过编辑 yaml 为特定的工作负载开启 Sidecar 自动注入，如有需要，您可以在 Pod 上添加 label：`istio.io/rev：{istio 版本号}`（注意 Sidecar 注入相关的标签设置，TCM 与 istio 默认语法略有区别），示例如下：

![](https://staticintl.cloudcachetci.com/yehe/backend-news/EGez825_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230217162808.png)

如果您需要为已经开启了自动注入的 Namespace 下的特定 Pod 添加特例，使其不自动注入 Sidecar，可在 Pod label 中添加：`sidecar.istio.io/inject="false"`。Pod 级别的注入开关优先级高于 Namespace 级别，关于 Sidecar 自动注入的更多细节，请参考 Istio 文档 [安装 sidecar](https://istio.io/latest/zh/docs/setup/additional-setup/sidecar-injection/)。

## 不拦截指定网段的流量

如果您不希望拦截某些流量，例如上传文件到 COS 对象存储存储的流量（169.254 开头的内网目标 IP），如果被拦截，且下载的文件较大，则可能导致 Sidecar 内存资源占用很高，因为 Sidecar 会缓存请求内容，出错自动重试时会复用请求内容。这时，您可以在网格基本信息页中的高级设置中配置“外部请求绕过Sidecar”，添加不希望拦截的网段。操作步骤如下：
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。

2. 在基本信息页面，单击**外部请求绕过Sidecar**右侧的![](https://qcloudimg.tencent-cloud.cn/image/document/5377020ec446cff9f40fc50aff12e406.png)。如下图所示：![](https://staticintl.cloudcachetci.com/yehe/backend-news/IbML391_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111165043.png)

3. 在“编辑外部请求绕过Sidecar”弹窗中，添加您不希望拦截的网段。如下图所示：![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bbrf780_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111165143.png)

4. 单击**保存**。


   以上是全局配置，如果希望只针对某些工作负载，可以给 Pod 添加注解 `traffic.sidecar.istio.io/excludeOutboundIPRanges` 。详情可参考 [注解列表](https://istio.io/latest/docs/reference/config/annotations/)。


   ![](https://qcloudimg.tencent-cloud.cn/image/document/f623dc7dcc2898781e4fb5c6e9f19f52.png)


## 控制 sidecar 启动顺序

Kubernetes 拉起 Pod 的时候是各个容器同时拉起，使用 istio 的场景，因为流量会被 Sidecar 拦截，当遇到 Sidecar 比业务容器启动更慢的时候，业务容器刚启动时的网络请求将会失败，因为流量被 Sidecar 拦截但 Sidecar 还没启动就绪。比较常见的场景是：集群规模较大，Sidecar 启动时拉取 xds 较慢导致 Sidecar 启动较慢，而业务进程启动时要从注册中心拉取配置，由于流量被 Sidecar 拦截而 Sidecar 此时还无法处理流量导致配置拉取失败，然后业务进程报错退出，导致容器退出。

主要有两种解决方案，第一种是让业务代码更健壮，启动时请求失败要不断重试，直至成功；第二种是让 Sidecar 先启动，等 Sidecar 就绪后再拉起业务容器。您可以参考以下步骤开启 Sidecar 就绪保障。

1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。

2. 在基本信息页面，单击 **Sidecar 就绪保障**右侧的![](https://qcloudimg.tencent-cloud.cn/image/document/a91192394184c5f2b8ac50475c3e5c2b.png)。如下图所示：


   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/NzxP537_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111165956.png)


   以上是全局配置，如果只想针对某些工作负载，可以为 Pod 添加如下注解：

   ``` yaml
   proxy.istio.io/config: '{ "holdApplicationUntilProxyStarts" : true }'
   ```

   ![](https://qcloudimg.tencent-cloud.cn/image/document/1915346cc8b1e0584577a0cf57dd52bf.png)


## Sidecar 优雅终止

业务发版时，工作负载滚动更新，Pod 在终止过程中，Sidecar 默认只等待几秒然后就会强制停止，如果业务请求本身耗时较长，或者使用长连接，可能会导致部分正常业务请求和连接中断，我们希望 Sidecar 会等待存量的业务请求和连接结束再退出以实现优雅终止。自 istio 1.12 开始，Sidecar 支持了 `EXIT_ON_ZERO_ACTIVE_CONNECTIONS`这个环境变量，作用就是等待 Sidecar “排水” 完成，在响应时，也通知客户端去关闭长连接（对于 HTTP1 响应 “Connection: close” 这个头，对于 HTTP2 响应 GOAWAY 这个帧）。您可以参考以下步骤开启 Sidecar 停止保障。
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。

2. 在基本信息页面，单击 **Sidecar 停止保障**右侧的![](https://qcloudimg.tencent-cloud.cn/image/document/75e5463109b558ebd4590411b9020fea.png)。如下图所示：![](https://staticintl.cloudcachetci.com/yehe/backend-news/iIPT551_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111170126.png)


   以上是全局启用的方法，通常也建议全局启用，如果只想针对某些工作负载开启，也可以为 Pod 添加如下注解：

   ``` yaml
   proxy.istio.io/config: '{ "proxyMetadata": { "EXIT_ON_ZERO_ACTIVE_CONNECTIONS": "true" } }'
   ```

   ![](https://qcloudimg.tencent-cloud.cn/image/document/2d65720805b03c6e4e399855d00f4170.png)


## 自定义 sidecar 资源

Sidecar 作为 Pod 中的一个 container，也需要设置 request 和 limit，如有需要，也可以自定义，您可以在网格基本信息页的高级设置中可以进行全局自定义。操作步骤如下：
1. 登录 [服务网格控制台](https://console.cloud.tencent.com/tke2/mesh)，单击需要变更配置的网格 ID，进入网格的管理页面。

2. 在基本信息页面，单击**自定义 sidecar 资源**右侧的![](https://qcloudimg.tencent-cloud.cn/image/document/53cece04b1422149aba317d0f4b590b7.png)。如下图所示：


   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/C9aQ307_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111170227.png)

3. 在“自定义 sidecar 资源”弹窗中，编辑自定义资源。如下图所示：


   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/68ep508_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230111170315.png)

4. 单击**保存**。


   如果希望对不同工作负载进行不同的自定义，也可以为 Pod 添加类似如下的注解：

   ``` yaml
   sidecar.istio.io/proxyCPU: "0.5"
   sidecar.istio.io/proxyCPULimit: '2'
   sidecar.istio.io/proxyMemory: "256Mi"
   sidecar.istio.io/proxyMemoryLimit: '2Gi'
   ```

   ![](https://qcloudimg.tencent-cloud.cn/image/document/ba20042b6d7f9122d7ac4d2ca63b3b3f.png)


   如果使用了 TKE Serverless，不希望因 Sidecar 的 request 和 limit 导致 Pod 规格变高很多，可以用注解只设置 request 不设置 limit，request 根据实际需要填写，填 “0” 就表示 Pod 规格完全不会因 Sidecar 而升配：

   ``` yaml
   sidecar.istio.io/proxyCPU: "0"
   sidecar.istio.io/proxyMemory: "0"
   ```

