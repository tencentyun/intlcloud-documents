## 操作场景

本文介绍如何管理集群中的虚拟节点节点池，包括如何调整虚拟节点池和调整节点池中的虚拟节点。

## 前提条件

- 请确保已经 [创建集群](https://intl.cloud.tencent.com/document/product/457/30637)。
- 请确保集群 Kubernetes 版本为 1.16 及以上版本。
- 集群中已有类型为“虚拟节点”的节点池。
- 建议阅读 [虚拟节点 Pod 调度说明](https://intl.cloud.tencent.com/document/product/457/39760)。

## 调整虚拟节点节点池
### 管理虚拟节点节点池
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**集群**。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的**节点管理**>**节点池**，进入“节点池列表”页面。如下图所示：
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. 选择计划修改的类型为**虚拟节点**的节点池，单击**编辑**。
5. 进入节点池编辑页面，支持修改节点池名称、Labels、Taints 等信息。如下图所示：
>! Labels、Taints 相关的修改会在节点池中的所有虚拟节点上生效，如果有特殊调度策略请务必谨慎操作。
>
![](https://main.qcloudimg.com/raw/82c7582937d53291993dac45dd1fc7c8.png)

### 删除虚拟节点节点池
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**集群**。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的**节点管理**>**节点池**，进入“节点池列表”页面。如下图所示：
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. 选择计划修改的类型为**虚拟节点**的节点池中的**更多**>**删除**。如下图所示：
![](https://main.qcloudimg.com/raw/38a8adb117764e1fd7df8c332e4c6e44.png)
5. 进入节点池删除确认页面，单击**确认**删除节点池。如下图所示：
>! 虚拟节点上如果有运行中的 Pod 则不可删除。勾选强制删除，则会驱逐重建节点池上的所有 Pod，请务必保证所有 Pod 可以重新调度到其他节点池上。
>
![](https://main.qcloudimg.com/raw/1fe5613c4695322373025632319e04bb.png)

## 调整虚拟节点
### 新建虚拟节点
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**集群**。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的**节点管理**>**节点池**，进入“节点池列表”页面。如下图所示：
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. 选择计划修改的类型为**虚拟节点**的节点池，单击节点池 ID 进入节点池详情页，可以进行基本信息编辑、新增/删除虚拟节点以及对具体虚拟节点进行驱逐、封锁/取消封锁等操作。如下图所示：
![](https://main.qcloudimg.com/raw/c31042c6068e6c1c8283d8c1e270b634.png)
5. 在节点池详情页中单击**新建节点**，可在当前节点池新增虚拟节点，只需指定新增虚拟节点关联的 VPC 子网，请保证指定子网可用 IP 数量充足。如下图所示：
>! 新增的虚拟节点会沿用节点池的 VPC、安全组、Labels、Taints 等一系列配置。
>
![](https://main.qcloudimg.com/raw/6b6f53971ab953a352c3bc5e76877c27.png)


### 移出虚拟节点
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**集群**。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的**节点管理**>**节点池**，进入“节点池列表”页面。如下图所示：
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. 选择计划修改的类型为**虚拟节点**的节点池，单击节点池 ID 进入节点池详情页。
5. 在节点池详情页中，单击**移出**删除选定的虚拟节点。如下图所示：
>! 虚拟节点上如果有运行中的 Pod 则不可删除。勾选强制删除，则会驱逐重建虚拟节点上的所有 Pod，请务必保证所有 Pod 可以重新调度到其他节点上。
>
![](https://main.qcloudimg.com/raw/1fe5613c4695322373025632319e04bb.png)


### 管理虚拟节点
1. 登录 [容器服务控制台](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的**集群**。
2. 在“集群管理”列表页面，选择目标集群 ID，进入该集群 “Deployment” 页面。
3. 选择左侧菜单栏中的**节点管理**>**节点池**，进入“节点池列表”页面。如下图所示：
   ![](https://main.qcloudimg.com/raw/305eb2bb4f470150d0c0ee3d2c76d7a7.png)
4. 选择计划修改的类型为**虚拟节点**的节点池，单击节点池 ID 进入节点池详情页。 
5. 单击虚拟节点名称进入虚拟节点详情页，可以管理虚拟节点上的 Pod、查看虚拟节点事件、Yaml 等信息。如下图所示：
![](https://main.qcloudimg.com/raw/e33c4df8ab26e13a4038cc65842618bf.png)

