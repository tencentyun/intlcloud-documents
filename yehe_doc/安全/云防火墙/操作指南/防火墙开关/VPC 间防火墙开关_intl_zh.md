## 操作场景
云防火墙开关提供 VPC 间防火墙开关功能，通过建立防火墙实例来承载不同 VPC 之间的访问流量，提供访问控制规则和日志审计系统。

当前版本的 VPC 间防火墙支持专线网关的防护，基于防火墙实例支持 CCN 多路由云联网模式，专线网关通过云联网与云上 VPC 资产建立连接，那么VPC间防火墙支持对这部分流量进行检测。

本文将介绍如何在 VPC 间开关页面，创建防火墙实例、查看带宽使用情况、规格信息以及查看网络拓扑和防火墙开关等操作。


## 查看状态监控
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch/vpc)，在左侧导航栏中，选择**防火墙开关** > **VPC 间开关**，进入 VPC 间开关页面。
2. 在 VPC 间开关页面的状态监控模块中，可以查看带宽使用情况，包括地域内峰值带宽、地域间峰值带宽、总的带宽规格等信息。
3. 在状态监控模块中，单击左上角的![](https://qcloudimg.tencent-cloud.cn/raw/cf118d35b3e8eb6b2d92b94f366bf7ef.png)，进入状态监控页面。
<img src="https://qcloudimg.tencent-cloud.cn/raw/d51d7dcbc249b9290cf329298b3dbea6.png" style="zoom:67%;" />
4. 在状态监控页面可以查看防火墙实例的带宽详情。支持按照时间和地域筛选实例的带宽统计情况。
![](https://qcloudimg.tencent-cloud.cn/raw/77ad513d860304784581a61a5cbf3518.png)
5. 也支持在防火墙实例页面，选择所需实例，单击**带宽监控**，可查看对应防火墙实例的带宽详情。
![](https://qcloudimg.tencent-cloud.cn/raw/94d14ceb314236c54f2df27fb99d11b7.png)

## 查看规格信息
在 [VPC 间开关页面](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=topo) 的规格信息模块中，可以查看规格信息，包括接入网络实例和 VPC 间防火墙实例。单击规则信息右上角的升级扩容，可以跳转到扩容界面。
![](https://qcloudimg.tencent-cloud.cn/raw/37246251957e00cd0d5c1c782228cded.png)

## 新建防火墙实例
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch/vpc)，在左侧导航栏中，选择**防火墙开关** > **VPC 间开关**，进入 VPC 间开关页面。
2. 在 VPC 间开关页面，单击**防火墙实例**，进入到防火墙实例页面，单击**创建实例**。
![](https://qcloudimg.tencent-cloud.cn/raw/2de9d33b72f21487dc526199d147729e.png)
3. 在新建 VPC 间防火墙弹窗中，根据需求选择好对应的模式，并选择模式。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e58d586821568c14bcf51e1d55d12675.png" style="zoom:67%;" />

**参数说明：**
- 实例名称：创建防火墙实例时自定义的名称。
- 模式：分为私有网络模式和云联网模式。
   - 私有网络模式：选择私有网络 VPC 接入防火墙，通过修改相关私有网络的路由表，来实现路由牵引。
   - 云联网模式：选择云联网 CCN 接入防火墙（需要支持多路由表模式），通过修改云联网路由表，来实现路由牵引。
 4. 根据模式的选择不同，所需填写的参数也不相同，具体操作如下所示：
- **私有网络模式**，
    1. 单击**下一步**，该页面展示了所有的 VPC 网络，勾选建立了网络连接的 VPC，单击**下一步**。
>!
>- 当前版本支持10个 VPC 私有网络，如需更多请 [提交工单](https://console.cloud.tencent.com/workorder/category) 申请。
>- 私有网络模式需要在所有选择接入的 VPC 地域创建防火墙实例。
>- 接入防火墙之前，需要确认 VPC 间已经创建对等链接/云联网，如果 VPC 之间没有建立连接，创建 VPC 防火墙不生效。

<img src="https://qcloudimg.tencent-cloud.cn/raw/e33b7807bd57f1f750cf6c5c727067fb.png" style="zoom:50%;" />

   2. 为每个 VPC 所属的地域创建防火墙实例。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f141e4017104cce2e2568699aeec21eb.png" style="zoom: 50%;" />
**字段说明：**
- 地域：接入防护的 VPC 所属的地域。
- 异地灾备：VPC 间防火墙支持异地灾备，通过勾选来开启。
<img src="https://qcloudimg.tencent-cloud.cn/raw/dbadaac8842ffc3abf78d3a10207c75d.png" style="zoom: 80%;" />
- 可用区：根据需求选择合适的可用区。
- 实例带宽：目前最小1024，最大3072，支持 [升级扩容](https://buy.cloud.tencent.com/cfw?type=modify&adtag=cfw.from.console.page.buy)。如果不满足最大带宽可创建多个防火墙实例。
- **云联网模式**
   1. 单击**下一步**，选择需要加入 VPC 防火墙的云联网实例，单击**下一步**。
>!
>- 需要云联网实例支持多路由表模式，如未满足请先联系云联网开启多路由表功能。
>- 云联网模式支持在指定地域创建 VPC 间防火墙。

 <img src="https://qcloudimg.tencent-cloud.cn/raw/0ce84413523235ce98ecfdaed219736d.png" style="zoom:67%;" />
   2. 防火墙实例部署地域分为单地域和全部地域，根据实际需求选择，并填写相关参数。
      - 单地域：选择一个地域部署防火墙实例，所有开启了防火墙开关的 VPC 间流量都会经过该地域的防火墙实例，适合**星形拓扑结构**的业务网络。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2807c86e452627022f837b02ac79563d.png" style="zoom:67%;" />
      - 全部地域：选择全部地域部署防火墙实例，开启了防火墙开关的 VPC 间流量都会经过本地域的防火墙实例，适合**网状拓扑结构**的业务网络。
<img src="https://qcloudimg.tencent-cloud.cn/raw/55e104bf93249c50088ea1c78e2a5554.png" style="zoom:67%;" />
5. 单击**完成**，完成配置，创建过程需要等待若干分钟。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6d5326b60360fe433f550682f6a2ef0.png" style="zoom:67%;" />

## 管理防火墙实例
防火墙实例创建完成后，可以对实例做一些操作，具体如下所示。

#### 查看配置详情
1. 在 [VPC 间开关页面](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance)，单击**防火墙实例 ID**或者是右侧的**详情**。
![](https://qcloudimg.tencent-cloud.cn/raw/407e9fd55abd8749a4727fa0b48c5738.png)
2. 在防火墙实例页面，在可以查看实例的相关配置详情。
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdc4b2f953c45b854a4843e155966df4.png" style="zoom:67%;" />

#### 查看防火墙开关
在 VPC 间开关页面，单击**更多** > **查看防火墙开关**，可以查看实例对应的防火墙开关。
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)

#### 销毁防火墙实例
1. 在 VPC 间开关页面，选择所需实例，单击防火墙开关处的**数字**。
![](https://qcloudimg.tencent-cloud.cn/raw/e9123fa7afb5a990af46ce9390995470.png)
2. 在防火墙开关页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/3ab29f514c114f26fdd157e67e15628a.png)关闭已开启的防护墙。
![](https://qcloudimg.tencent-cloud.cn/raw/8dc2d72fd080a2c78e1f85180561f886.png)
3. 在 VPC 间开关页面，单击**更多** > **销毁实例**。
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
4. 在确认销毁弹出中，单击**确定**，即可销毁所选实例。
>? 销毁实例后，对应地域的 VPC 间防火墙实例将被回收，所有数据将清除，您的 VPC 间防火墙配额将会归还，系统会自动还原网络和路由设置。

#### 重新选择接入实例
1. 在 VPC 间开关页面，选择所需实例，单击防火墙开关处的**数字**。
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
2. 在防火墙开关页面，单击![](https://qcloudimg.tencent-cloud.cn/raw/3ab29f514c114f26fdd157e67e15628a.png)关闭已开启的防护墙。
![](https://qcloudimg.tencent-cloud.cn/raw/d3b4bc3fe31d92ab387bb624d6057781.png)
3. 在防火墙开关页面，单击 **更多** > **重新选择接入实例**，进入编辑 VPC 间防火墙页面。
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
4. 在编辑 VPC 间防火墙页面，选择所需实例，单击**下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e33b7807bd57f1f750cf6c5c727067fb.png" style="zoom:50%;" />
5. 选择选择部署的地域/可用区，单击**完成**，即可完成重新选择接入的实例。
>? 异地灾备：勾选后，支持将主机和备机防火墙部署在不同可用区。

<img src="https://qcloudimg.tencent-cloud.cn/raw/f141e4017104cce2e2568699aeec21eb.png" style="zoom:50%;" />

## 查看网络拓扑
云防火墙提供了一个可视化视图，帮助您快速梳理 VPC间资产的访问关系，具体操作如下所示。
1. 在 [VPC 间开关页面](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance)，单击**网络拓扑**，查看接入的 VPC 网络实例详情。
2. 在网络拓扑页面，鼠标悬停在某个 VPC 实例，可以查看该实例的详细信息。
 ![](https://qcloudimg.tencent-cloud.cn/raw/614abcc954f8ef0d959b46fc510e0c37.png)
3. 单击**某个实例**，可查看与其他 VPC 实例的连接情况，以及防火墙开关开启情况。防火墙开关标识如果深蓝色则代表开关开启，如果是灰色则代表开关关闭。
 ![](https://qcloudimg.tencent-cloud.cn/raw/7126e1c984ca635cb99eb89c5ca65d83.png)
4. 在网络拓扑页面，单击**同步资产**，可以及时同步资产信息；将鼠标悬停引擎更新处可以查看版本信息。
![](https://qcloudimg.tencent-cloud.cn/raw/00711982e1916edd98a28ae52f3e815a.png)
5.在网络拓扑页面，单击右上角的![](https://qcloudimg.tencent-cloud.cn/raw/fa802f285d939de86e97a900df3711fb.png)或![](https://qcloudimg.tencent-cloud.cn/raw/1852ba95aae284de29263fa834546225.png)，可查看操作指引或刷新网络拓扑。


## 管理防火墙开关
在防火墙开关页面，可通过开启或者关闭 VPC 间防火墙的开关，来实现对 VPC 间流量的管控。同时云防火墙会自动同步资产，因此不用担心资产变更后防火墙配置的问题，云防火墙在短时间内会自动同步。
>! 开启/关闭防火墙操作涉及网络和路由切换，将会产生短时间网络抖动和闪断，请合理选择操作时间。

#### 开启防护
开启开关后，系统会自动修改相关路由表的路由策略，将所有防火墙开关对应的本端和对端网络间的流量牵引至 VPC 间防火墙。
1. 在 [VPC 间开关页面](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance)，单击**防火墙开关**，支持单个或全部开启防火墙。
   - 单个：选择所需防火墙，单击防火墙开关的![](https://qcloudimg.tencent-cloud.cn/raw/5b2964b90d566c2fad62d7a8647060db.png)，弹出确认开启弹窗。
   ![](https://qcloudimg.tencent-cloud.cn/raw/4ad2d399655715fce5cc6a569362d310.png)
   - 全部：单击左上角的**全部开启**，弹出确认开启弹窗。
   ![](https://qcloudimg.tencent-cloud.cn/raw/6bf26f23792c3f127e615d79bd592556.png)
2. 在确认开启弹窗中，单击**确定**，即可开启防护。 

#### 关闭防护
关闭开关后，系统会自动恢复相关路由表的路由策略，所有防火墙对应的本端-对端网络间的流量将恢复原先路劲，不会经过 VPC 间防火墙。
1. 在 [VPC 间开关页面](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance)，单击**防火墙开关**，支持单个或全部关闭防火墙。
    - 单个：选择所需防火墙，单击防火墙开关的![](https://qcloudimg.tencent-cloud.cn/raw/d17747e4df84d5724919e7f8b54ff5f3.png)，弹出确认关闭弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/8dc2d72fd080a2c78e1f85180561f886.png)
    - 全部：单击左上角的**全部关闭**，弹出确认关闭弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/4b28612abcff0e4c5fadd526ae26c33f.png)
2. 在确认关闭弹窗中，单击**确定**，即可关闭防护。

#### 查看规则
1. 在防火墙开关页面，单击 **查看规则**，进入 VPC 间规则页面。
![](https://qcloudimg.tencent-cloud.cn/raw/0feb1e18e285f1c6344407744f5bcbbd.png)
2. 在 VPC 间规则页面，可以对规则进行查看和编辑，操作详情请参见 [访问控制-VPC 间规则](https://intl.cloud.tencent.com/document/product/1160/49846)。
![](https://qcloudimg.tencent-cloud.cn/raw/25a7fc2da4714a4e299b0224da94244c.png)

#### 查看日志
在防火墙开关页面，单击 **更多** > **查看日志**，可以选择查看流量访问控制日志或流量日志。
![](https://qcloudimg.tencent-cloud.cn/raw/c4466c7625cd63fafb9d280e945d9a62.png)


## 使用 VPC 视图梳理 VPC 间的访问关系
云防火墙提供了一个可视化视图，帮助您快速梳理 VPC 之间的访问关系。在 VPC 可视化视图中，每个节点是一个 VPC 实例，VPC 间防火墙是一个中心化的设备，为每一对互通的 VPC 配置了开关。已开启开关的 VPC 间流量将会被牵引至防火墙进行过滤与防护。
1. 登录 [云防火墙控制台](https://console.cloud.tencent.com/cfw/switch/vpc)，在左侧导航栏中，选择**防火墙开关** > **VPC 间开关**，进入 VPC 间开关页面。
2. 在  VPC 间开关页面，单击**网络拓扑**，进入网络拓扑页面。
3. 将鼠标在某个 VPC 节点上悬停，可查看 VPC 的简要信息，同时与之互联的所有 VPC 也会亮起。单击**私有网络 ID** 的蓝色字体，可进入 VPC 详情页查看该 VPC 的详细信息。
&nbsp;
![](https://qcloudimg.tencent-cloud.cn/raw/a37cfcd11adccbe271276724ccd713ee.png)
&nbsp;
4. 您可以单击某个 VPC 节点，页面进入聚焦视图，显示以聚焦 VPC 为中心的拓扑结构。
5. 彼此互通的 VPC 间通过连线相连接，连线中可以查看防火墙开关，您可以操作开关，也可以通过单击开关的图标，直接进入访问控制规则配置页面。
&nbsp;
![](https://qcloudimg.tencent-cloud.cn/raw/29d29c1792c8bf6c50b82512b893bc11.png)

## VPC 间防火墙的异常场景说明
- VPC 间防火墙在开启和关闭开关时，涉及后台自动修改您的路由策略，导致**在一个极短的时间内会出现网络闪断**，为不影响您的业务，请您合理安排操作 VPC 间防火墙开关的时间。如果需要进行批量或频繁的开关操作，建议在业务流量较小的深夜进行。
>? 互联网边界防火墙的开关不存在类似问题。

- VPC 间防火墙开关建立在 VPC 间的对等连接（或云联网）之上，若您变更（或删除）了对等连接（或云联网）的配置，则防火墙开关也会自动对应变更（或删除）。为了不影响您的业务，云防火墙只会对状态为关闭的开关立即执行变更（或删除）。
>?若您的云上资产有所变更（或删除），互联网边界防火墙开关会在短时间内（5分钟左右）自动同步。

- 若 VPC 间没有正在启用的路由，则防火墙开关无法开启。
>?如需配置对等连接路由，请参见 [配置指向对等连接的路由](https://intl.cloud.tencent.com/document/product/553/19696)。如需配置云联网路由，请参见 [路由概述](https://intl.cloud.tencent.com/document/product/1003/34259)。

- 云防火墙开关开启状态下，**在 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 手动变更对应 VPC 路由表属于高危操作**，由于云防火墙无法同步路由的变更，可能导致防火墙失效，网络连接中断。
- 云防火墙开关关闭状态下，您可以根据需要切换 VPC 间的其他对等连接（或云联网）路由，但**请勿启用备注信息为“防火墙”的路由**，否则将导致网络连接中断，防火墙开关故障。


## 相关信息
- 如需对所持有的公网 IP 以及关联的云上资产，配置对应的防火墙开关，可参见 互联网边界防火墙开关进行操作。
- 如需对内网资产进行流量管控与安全防护，或基于 SNAT、DNAT 进行的网络流量转发，可参见 [NAT 边界防火墙开关](https://intl.cloud.tencent.com/document/product/1160/49810) 进行操作。
- 如遇到 VPC 间防火墙相关问题，可参见 [VPC 间防火墙](https://intl.cloud.tencent.com/document/product/1160/49830) 文档。
