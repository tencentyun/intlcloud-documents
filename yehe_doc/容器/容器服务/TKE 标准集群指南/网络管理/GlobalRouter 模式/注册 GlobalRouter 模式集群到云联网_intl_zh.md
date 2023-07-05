## 云联网说明
[云联网（Cloud Connect Network，CCN）](https://intl.cloud.tencent.com/document/product/1003/30049) 为您提供云上私有网络间（Virtual Private Cloud，VPC）、VPC 与本地数据中心间互联的服务。您可以将 VPC 和专线网关实例加入云联网，以实现单点接入、全网资源互通，轻松构建简单、智能、安全、灵活的混合云及全球互联网络。


## 操作场景
您可以将已有容器集群注册到云联网，云联网可将容器网络归纳至管理范围中。当容器网络完成注册后，您可以在云联网侧启用或关闭容器网络的网段路由，实现容器集群与云联网内的资源互通。
>!当容器集群注册到云联网后，该网段与云联网实例中已有路由不冲突时开启，冲突时默认关闭。





## 前提条件
- 集群所在 VPC 已在云联网中，云联网相关操作请参见 [云联网操作总览](https://intl.cloud.tencent.com/document/product/1003/30061)。
- 评估集群容器网络的网段是否与云联网网内其他资源网段冲突。


## 操作步骤

### 注册容器网络至对应云联网
1. 登录容器服务控制台，单击左侧导航栏中的**[集群](https://console.cloud.tencent.com/tke2/cluster)**进入集群管理页面。
2. 选择需要进行云联网注册的集群 ID，单击左侧的**基本信息**进入集群基础信息页面。
3. 单击云联网的注册开关，将容器网络注册到云联网。如下图所示：
>!此步骤仅是将容器网段注册到云联网，路由是否生效，需要在云联网侧控制。
>
![](https://main.qcloudimg.com/raw/0615d4b5ac0c3dd42e8ff28b2b350c41.png)




### 查看容器网段路由
1. 登录私有网络控制台，单击左侧导航栏中的**[云联网](https://console.qcloud.com/vpc/ccn)**进入云联网管理页面。
2. 单击集群 VPC 关联的云联网所在行右侧的**管理实例**，进入云联网实例管理页面。如下图所示：
![](https://main.qcloudimg.com/raw/1612987cc3aa60ea57ac284b7b61ccfa.png)
3. 在云联网实例管理页面中，单击**路由表**页签，查看容器网段路由启动情况。如下图所示：
>?
>- 若网段不冲突，则路由默认启动。网段冲突，则路由默认关闭。
>- 路由冲突原则请参见 [路由限制](https://intl.cloud.tencent.com/document/product/1003/30052)，如需启动冲突路由，请参见 [启用路由](https://intl.cloud.tencent.com/document/product/1003/30069)。
>
![](https://main.qcloudimg.com/raw/0d7beab6c11c1c22f2ebcd20fc93f7f9.png)
4. 可开始测试容器集群与云联网其他资源的互通性。














