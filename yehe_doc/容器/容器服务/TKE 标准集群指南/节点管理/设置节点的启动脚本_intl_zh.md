## 操作场景
设置节点的启动脚本可以帮助您在节点 ready 之前，对您的节点进行初始化工作，即当节点启动的时候运行配置的脚本，如果一次购买多台云服务器，自定义数据会在所有的云服务器上运行。

## 使用限制

- 建议您不要通过启动脚本修改 TKE 节点上的 Kubelet、kube-proxy、docker 等配置。
- 启动脚本执行失败不重试，需自行保证脚本的可执行性和重试机制。
- 脚本及其生成的日志文件可在节点的  `/usr/local/qcloud/tke/userscript` 路径查看。

## 操作步骤

您可以在以下三个场景设置节点的启动脚本：
- [创建集群或新增节点时，设置节点的启动脚本](#CreateClusterOrCreateNode)
- [添加已有节点时，设置节点的启动脚本](#CreateCVM)
- [创建伸缩组时，设置节点的启动脚本](#CreateFlexGroup)

<span id="CreateClusterOrCreateNode"></span>
### 创建集群或新增节点时，设置节点的启动脚本
- [创建集群](https://intl.cloud.tencent.com/document/product/457/30637) 时，在 “云服务器配置” 页面，单击**高级设置**，填写自定义数据，启动脚本。如下图所示：
![](https://main.qcloudimg.com/raw/fd22ee1caca15449ea74114d5462c6a4.png)
- [新增节点](https://intl.cloud.tencent.com/document/product/457/30652) 时，在 “云服务器配置” 页面，单击**高级设置**，填写自定义数据，启动脚本。如下图所示：
![](https://main.qcloudimg.com/raw/7b793fca3791823d14c45d17df6aa106.png)

<span id="CreateCVM"></span>
### 添加已有节点时，设置节点的启动脚本
[添加已有节点](https://intl.cloud.tencent.com/document/product/457/30652#addExistingNode) 时，在 “云服务器配置” 页面，单击**高级设置**，填写自定义数据，启动脚本。如下图所示：
![](https://main.qcloudimg.com/raw/94f828deadbc7bfc4d9ed8357ddfc84d.png)

<span id="CreateFlexGroup"></span>
### 创建伸缩组时，设置节点的启动脚本
[创建伸缩组](https://intl.cloud.tencent.com/document/product/457/30638) 时，在 “启动配置” 页面，单击**高级设置**，填写自定义数据，启动脚本。如下图所示：
![](https://main.qcloudimg.com/raw/13fb463e4ea280910701110ab20b09ab.png)




