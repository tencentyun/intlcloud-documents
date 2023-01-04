本文档为您介绍集群资产功能，以及如何查看集群、Pod、Service、Ingress 资产详情。
![](https://qcloudimg.tencent-cloud.cn/raw/924b5267259984da67c46c43d0551c1c.png)

## 查看集群模块
集群模块展示了集群总数以及每种集群类型的数量。

### 查看集群列表
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中，单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击**“集群总数”**，进入集群检查页面，可查看全部集群资产。
![](https://qcloudimg.tencent-cloud.cn/raw/5fb66207dc0d1d99a596cac9e99436b1.png)
3. 在集群检查页面，单击**搜索框**，通过“集群名称、集群 ID、集群类型、所属地域”等关键字可对集群进行查找。
![](https://qcloudimg.tencent-cloud.cn/raw/6dc4430d80be2bd18fafc01d211eaf70.png)

### 自定义列表管理
1. 在集群检查页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png)图标，弹出自定义列表管理对话框。
2. 在自定义列表管理对话框，选择所需的类型后，单击**确定**，即可完成设置自定义列表。
![](https://qcloudimg.tencent-cloud.cn/raw/cb76f083f243b760442eb5311fd9e71f.png)

## 查看 Pod 模块
Pod 模块展示了集群 Pod 总数，以及 Running、Pending 状态的 Pod 数量。

### 查看 Pod 列表
1. 在资产管理页面，单击**“Pod 总数”**，进入 Pod 列表页面，可查看全部 Pod 资产。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7293bb60448a089708a62d6ebd05578a.png" style="zoom:80%;" />
2. 在 Pod 列表页面，可按“集群名称、命名空间、地域”对 Pod 资产进行筛选；单击**更多筛选**可按“Pod 状态、工作负载类型、工作负载名称、集群 ID、Pod IP、所在节点 IP、容器名称、容器 ID、镜像名称”对 Pod 资产进行筛选；或单击**搜索框**通过“Pod 名称”关键字可对 Pod 资产进行查找。
![](https://qcloudimg.tencent-cloud.cn/raw/ec1218e09f2c650b8ffe913db6daccc3.png)
3. 找到目标 Pod，单击 **Pod 名称**，右侧弹出抽屉展示该 Pod 详情，页面可切换查看 Pod 基本信息、Service 和容器等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/91636c57327aa64ac379ae67c45f5ebb.png)

### 自定义列表管理
1. 在 Pod 列表页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png)图标，弹出自定义列表管理对话框。
2. 在自定义列表管理对话框，选择所需的类型后，单击**确定**，即可完成设置自定义列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/751087386ce5677bea89a6558e1a9803.png" style="zoom:80%;" />

## 查看 Service 模块
Service 模块展示了集群 Service 总数，以及 ClusterIP、NodePort 类型的 Service 数量。

### 查看 Service 列表
1. 在资产管理页面，单击**“Service 总数”**，进入 Service 列表页面，可查看全部 Service 资产。
<img src="https://qcloudimg.tencent-cloud.cn/raw/5eabffc28ba9427a82f80b423a8c8410.png" style="zoom:80%;" />
2. 在 Service 列表页面，可按“集群名称、命名空间、地域”对 Service 资产进行筛选，单击**更多筛选**可按“集群 ID、Service 类型、负载均衡 IP、服务 IP、Labels、端口”对 Service 资产进行筛选。或单击**搜索框**通过“Service 名称”关键字可对 Service 资产进行查找。
![](https://qcloudimg.tencent-cloud.cn/raw/cc0baecfb0d27d6a37c2bb9272fed4a1.png)
3. 找到目标 Service，单击**“Service 名称”**，右侧弹出抽屉展示该 Service 详情，页面可切换查看 Service 基本信息、Pod、YAML 和端口映射规则等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/3af7e3324dd3a4f4a5d174b5ce828d9a.png)

### 自定义列表管理
1. 在 Service 列表页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png)图标，弹出自定义列表管理对话框。
2. 在自定义列表管理对话框，选择所需的类型后，单击**确定**，即可完成设置自定义列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/5558fd9a87c2b7d099380f1a8f9cebb9.png" style="zoom:80%;" />

## 查看 Ingress 模块
Ingress 模块展示了集群 Ingress 总数。

### 查看 Ingress 列表
1. 在资产管理页面，单击**“Ingress 总数”**，进入 Service 列表页面，可查看全部 Ingress 资产。
<img src="https://qcloudimg.tencent-cloud.cn/raw/4de8c84beb002b7f0052650a5e50f3f3.png" style="zoom:80%;" />
2. 在 Ingress 列表页面，可按“集群名称、命名空间、地域”对 Ingress 资产进行筛选；单击**更多筛选**可按“Ingress 名称、VIP、Labels、后端服务”对 Ingress 资产进行筛选；或单击**搜索框**通过“Ingress 名称”关键字可对 Ingress 资产进行查找。
![](https://qcloudimg.tencent-cloud.cn/raw/349d3d3ab0343023feb6b50ba1e41987.png)
3. 找到目标 Ingress，单击**“Ingress 名称”**，右侧弹出抽屉展示该 Ingress 详情，页面可切换查看 Ingress 基本信息、转发配置和 YAML 信息。
![](https://qcloudimg.tencent-cloud.cn/raw/3229161beba3f95b003e5dee6a7e907f.png)


### 自定义列表管理
1. 在 Ingress 列表页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/131751ce4e643d8bc382f8b0bb316beb.png)图标，弹出自定义列表管理对话框。
2. 在自定义列表管理对话框，选择所需的类型后，单击**确定**，即可完成设置自定义列表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/336f38bdb675f2e8113d7621216d1bf8.png" style="zoom:80%;" />
