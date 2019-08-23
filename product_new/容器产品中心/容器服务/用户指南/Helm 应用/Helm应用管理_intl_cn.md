## 操作场景

您可以通过控制台管理 Helm 应用的创建、删除、修改等操作，也可以通过本地安装 Helm 客户端连接到集群后，通过 Helm 命令行进行操作。

## 前提条件

- 已有腾讯云 TKE 集群，且拥有0.28核 CPU，180MiB内存的资源。
- 已在集群内开通 Helm 应用管理功能。
- 仅支持kubernetes 1.8以上版本的集群
>- 若未开通 Helm 应用管理功能，请在 [Helm 应用](https://console.cloud.tencent.com/tke2/helm) 中，申请开通。
> - 开通 Helm 应用管理功能后，将在集群内安装 Helm tiller 相关组件。

 ![](https://main.qcloudimg.com/raw/1be3fceade676e04d3db457862e2c5ea.png)

## 操作步骤

### 创建 Helm 应用

1. 登录 [腾讯云容器服务控制台](https://console.cloud.tencent.com/tke2)。
2. 在左侧导航栏中，单击【[Helm 应用](https://console.cloud.tencent.com/tke2/helm)】，进入 Helm 应用管理页面。
3. 单击【新建】，进入 “新建 Helm 应用” 页面。
4. 输入应用名、Chart_Url, 选择 Helm Chart 来源的类型：公开和私有两种。如下图所示：
 ![](https://main.qcloudimg.com/raw/87257d2d7c8c64f93ea4e4f3240547ba.png)
 Helm Chart 来源 “other” 可选择为以下两种：
 -  Helm 官方仓库
 -  自建 Helm Repo 仓库。
>当 Helm Chart 来源为 “其他” 类型时，Chart_url 属性必须设置为以 http 开头 tgz 结尾的参数值。
5. 单击【完成】。

### 更新 Helm 应用

1. 前往 [Helm 应用控制台](https://console.cloud.tencent.com/tke2/helm)。
2. 在 “Helm应用” 列表中，选择需要更新的 Helm 应用，单击【更新应用】。
3. 在弹出的 “更新Helm应用” 窗口中，手动填写Chart_url版本号。如下图所示：
![](https://main.qcloudimg.com/raw/57a64278507ced270c489f863c9dbf2c.png)
4. 单击【完成】。

### 回滚 Helm 应用

1. 前往 [Helm 应用控制台](https://console.cloud.tencent.com/tke2/helm)。
2. 在 “Helm应用” 列表中，单击需要更新的 Helm 应用的应用名，进入应用详情页面。
3. 选择 “版本历史” 页签，在需要回滚的版本行中，单击【回滚】。

### 删除 Helm 应用

1. 前往 [Helm 应用控制台](https://console.cloud.tencent.com/tke2/helm)。
2. 在 “Helm应用” 列表中，选择需要删除的 Helm 应用，单击【删除】。
3. 在弹出的提示框中，单击【确认】。如下图所示：
![](https://main.qcloudimg.com/raw/90f2f47a828d75d7494f2ac749495746.png)

