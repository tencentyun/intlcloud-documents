## 远程终端连接到容器
1. 登录腾讯云容器服务控制台，选择左侧导航栏中的 **[集群](https://console.cloud.tencent.com/tke2/cluster)** 。
2. 在“集群管理”页面，单击集群 ID（cls-xxx），进入集群基本信息页。
3. 选择左侧导航栏中的**节点管理 > 节点**。在“节点列表”页面，单击节点 ID，进入 Pod 管理页面。
4. 在实例列表中，单击实例右侧的**远程登录**。如下图所示。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/CgXp682_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221223160402.png)
<dx-alert infotype="notice" title="">
符合以下任一条件的容器均不支持远程登录：
- 命名空间为 kube-system。
- 容器镜像中没有内置 bash。
更多远程终端常见问题单击 [查看详情](https://intl.cloud.tencent.com/document/product/457/8638)。
</dx-alert>
5. 在容器登录弹窗中选择 Shell 环境，单击容器右侧的**登录**。


## 未安装 shell 的容器运行命令
1. 进入远程终端页面。
2. 在下方输入要执行的命令，单击**Enter**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/68d5298797ff405816af9bf74e169f44.png)

## 文件的上传与下载
1. 进入远程终端页面。
2. 单击下方的**File**，选择上传或下载文件。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/1869cf17e59d25858c8fe44abe0a59f6.png)
 - **Upload File**：上传需指定上传的文件目录。
 - **Download File**：下载需指定下载的文件的路径。


