本文向您介绍如何使用容器服务快速创建一个容器集群。


## 步骤1：注册腾讯云账号
在使用腾讯云容器服务之前，您需要 [注册腾讯云账号](https://www.tencentcloud.com/account/register?s_url=https%3A%2F%2Fconsole.tencentcloud.com%2Ftke2%2Fcluster%3Frid%3D1) 并完成 [实名认证](https://www.tencentcloud.com/document/product/378/3629)。

## 步骤2：在线充值
腾讯云容器服务 TKE 针对不同规格的托管集群，会收取相应的集群管理费用，以及用户实际使用的云资源费用。关于收费模式和具体价格，请参阅 [容器服务计费概述 ](https://intl.cloud.tencent.com/document/product/457/45157)。本文中我们创建的是“托管集群”，该模式下您依然要为集群的工作节点、持久化存储以及服务绑定的负载均衡等服务付费。购买前，需要在账号中进行充值。具体操作请参考 [在线充值](https://intl.cloud.tencent.com/document/product/555/7425) 文档。



## 步骤3：服务授权
在 [腾讯云控制台](https://console.cloud.tencent.com/) 中，选择**云产品** > **容器服务**，进入容器服务控制台，按照界面提示为容器服务授权。（如果您已为容器服务授权，请跳过该步骤。）

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster?rid=1" target="_blank"  style="color: white; font-size:13px;">点此进行服务授权</a></div>


## 步骤4：新建集群
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tke2/cluster/create?rid=1" target="_blank"  style="color: white; font-size:13px;">点此进入创建集群页面</a></div>

### 集群信息
在“集群信息”页面，填写集群名称、选择集群所在地域、选择集群网络和容器网络，保持其他默认选项，并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/48966b45ba60fe9116bb58edec3c58dd.png)

 - **集群名称**：输入要创建的集群名称。本文以“test”为例。
 - **所在地域**：选择与您最近的一个地区，例如我在 “深圳”，地域选择 “广州”。
 - **集群网络**：为集群内主机分配在节点网络地址范围内的 IP 地址。这里我们选择已有的 VPC 网络。
 - **容器网络**：为集群内容器分配在容器网络地址范围内的 IP 地址。这里我们选择可用的容器网络。


### 选择机型
在“选择机型”页面，确认计费模式、选择可用区及对应的子网、确认节点的机型，并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/ef0eddd2e2a0ea044774c4ee65d0a2ef.png)

- **节点来源**：提供**新增节点**和**已有节点**两个选项。这里我们选择 “新增节点”。
- **集群类型**：提供**托管集群**和**独立集群**两种集群模式选择。这里我们选择 “托管集群”。
- **集群规格**：提供多种集群规格。这里我们选择 “L5”。
- **计费模式**：提供**按量计费**的计费模式。
- **Worker 配置**：该模块下只需选择可用区及对应的子网并确认节点的机型，其他设置项保持默认。
  - **可用区**：这里我们选择 “广州一区”。
  - **节点网络**：这里我们选择当前 VPC 网络下的子网。
  - **机型**：这里我们选择 “SA2.MEDIUM2(标准型SA2,2核2GB)”。

### 云服务器配置
在“云服务器配置”页面，选择登录方式，其他设置项保持默认，并单击**下一步**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/83501db19590eccb230c482ae37bd3a9.png)

- **登录方式**：提供**立即关联密钥**、**自动生成密码**和**设置密码**三种登录方式。这里我们选择 “自动生成密码”。

### 组件配置
在“组件配置”页面，组件包含存储、监控、镜像等，您可按需选择。若无需安装，可单击**下一步**。这里我们选择不安装组件，其他设置项保持默认。

### 信息确认
在“信息确认”页面，确认集群的已选配置信息和费用。当您阅读并同意容器服务服务等级协议后，单击**完成**。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/bebdbb0524ba191175daa935b9d7d986.png)


当您付费完成后，即可创建您的第一个集群。接下来，您可以在 [容器服务控制台](https://console.cloud.tencent.com/tke2/cluster?rid=1) 查看您已创建的 TKE 标准集群。

## 步骤5：查看集群
创建完成的集群将出现在 [集群列表](https://console.cloud.tencent.com/tke2/cluster?rid=1) 中。您可单击集群 ID 进入集群详情页面。在集群的“基本信息”页面中，您可查看集群信息、节点和网络信息、集群 APIServer 信息等。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/0f36c74372186d3efdf1ba2f1751f228.png)



## 步骤6：删除集群
集群启动后即开始消耗资源，为避免产生不必要的费用，此步骤向您介绍如何清除所有资源。

1. 选择左侧导航栏中的**集群**，在“集群管理”页面选择需删除集群所在行右侧**更多 > 关闭集群删除保护**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/iEGX674_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215175257.png)
2. 选择集群所在行右侧**更多 > 删除**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Pt9T223_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221215175351.png)
2. 在“删除集群”弹窗中确认信息后，单击**确定**即可删除集群。



## 后续操作：使用集群
通过本文，您已经了解如何在腾讯云容器服务中创建和删除集群。在已创建的集群中，您可以设置工作负载和创建服务。常用的任务包括：
- [创建简单的 Nginx 服务](https://intl.cloud.tencent.com/document/product/457/7851)
- [单实例版 WordPress](https://intl.cloud.tencent.com/document/product/457/7205)
- [使用 TencentDB 的 WordPress](https://intl.cloud.tencent.com/document/product/457/7447)
- [手动搭建 Hello World 服务](https://intl.cloud.tencent.com/document/product/457/7204)
- [构建简单 Web 应用](https://intl.cloud.tencent.com/document/product/457/6996)


## 遇到问题？
使用容器服务控制台创建标准集群的完整步骤请参考 [创建集群](https://intl.cloud.tencent.com/document/product/457/30637)。如果您在使用时遇到问题，您可以 [联系我们](https://intl.cloud.tencent.com/document/product/457/46720) 来寻求帮助。
