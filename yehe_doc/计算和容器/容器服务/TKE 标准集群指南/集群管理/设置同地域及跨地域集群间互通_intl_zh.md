## 操作场景
对等连接（Peering Connection）是一种大带宽、高质量的云上资源互通服务，可以打通腾讯云上的资源通信链路。请参考 [创建对等连接](https://intl.cloud.tencent.com/document/product/553/18836) 建立对等连接，您可以通过对等连接实现**同地域和跨地域**的不同集群互通。

>
>- 本文档以已创建集群并已添加节点为例。若未创建，请参考 [创建集群](https://intl.cloud.tencent.com/document/product/457/11741) 进行创建。
>- 请先确保对等连接成功建立，且子机间能互通。若对等连接建立有问题，请排查**控制台路由表项、CVM 安全组、子网 ACL** 的设置是否有问题。



## 操作步骤

>如需实现跨地域集群间互通，请在执行完以下操作步骤后 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1 ) 申请打通容器路由，实现容器间互通。

### 获取容器的基本信息
1. 登录容器服务控制台，选择左侧导航栏中的【[集群](https://console.cloud.tencent.com/tke2/cluster)】。
3. <span id="step3">单击需要设置集群间互通的集群 ID/名称，进入该集群的管理页面。如下图所示：</span>
例如，进入 A 集群的管理页面。
![](https://main.qcloudimg.com/raw/37757652cd5c8fe05452c961ce35020a.png)
4. 在左侧导航栏中，选择 “基本信息”，进入“基本信息” 页面。如下图所示：
![](https://main.qcloudimg.com/raw/7e0db2c6133f1c6b0af40dfc833147d3.png)
5. <span id="step5">记录 “基础信息” 中 “所在地域”、“节点网络” 和 “容器网络” 的信息。</span>
6. 重复执行 [步骤3](#step3) - [步骤5](#step5)，记录另一个集群容器 “所在地域”、“节点网络” 和 “容器网络” 的信息。
例如，记录 B 集群容器 “所在地域”、“节点网络” 和 “容器网络” 的信息。


### 配置路由表

1. 登录私有网络控制台，选择左侧导航栏中的【[对等连接](https://console.cloud.tencent.com/vpc/conn)】。
2. 在对等连接管理页面，记录对等连接的 **ID/名称**。
3. <span id="VPCStep3"></span>选择左侧导航栏中的【[子网](https://console.cloud.tencent.com/vpc/subnet)】，进入子网管理页面。
4. 单击对等连接本端指定子网的关联路由表。如下图所示：
![](https://main.qcloudimg.com/raw/fd61cd59e135f9f7de1b528a17a80779.png)
5. 在关联路由表的 “默认详情” 页面，单击【+新增路由策略】。
6. 在弹出的 “新增路由” 窗口中，设置路由信息。主要参数信息如下：
 - 目的端：输入 B 集群容器的网段。
 - 下一跳类型：选择 “**对等连接**”。
 - 下一跳：选择已建立的对等连接。
7. <span id="VPCStep7">单击【确定】，完成本端路由表的配置。</span>
8. 重复执行 [步骤3](#VPCStep3) - [步骤7](#VPCStep7)，完成对端路由表的配置。

## 预期结果
- **同地域集群**：通过上述操作可直接实现容器之间的互通。
- **跨地域集群**：对等连接建立成功后，请 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=350&source=0&data_title=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1TKE&step=1 ) 打通容器路由，实现容器之间的互通。

请参考 [远程终端基本操作](https://intl.cloud.tencent.com/document/product/457/9120) 登录容器，并按照以下步骤进行容器间的访问，验证容器间是否互通：
1. 登录集群 A 的容器，并在集群 A 的容器中访问集群 B 的容器。如下图所示：
![](https://main.qcloudimg.com/raw/18e74866a2bd8824b4537af65108b62a.png)
2. 登录集群 B 的容器，并在集群 B 的容器中访问集群 A 的容器。如下图所示：
![](https://main.qcloudimg.com/raw/6ec462617b4130cc73e088a8632a406e.png)
