## 背景信息
目前 VPC 专线接入暂时只支持亚太东南（新加坡），已经支持公有云与客户机房网络在 VPC 内互通，可以直接安装客户端。

若需要接入的地区不在 VPC 专线接入的范围之内，需要通过 [云联网](https://intl.cloud.tencent.com/document/product/1003/30049)，将专线网关（VPN）与 VPC 打通。专线网关需要客户另行 [购买](https://intl.cloud.tencent.com/document/product/1003/30053) 和搭建完成对 VPC 专线接入的工作。

## 操作指南
### 步骤1：确认是否需要通过云联网进行接入[](id:steps1)
1. 登录 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，在左侧导航中单击**资产管理**，进入资产管理页面。
2. 在资产管理页面，单击容器的**主机节点** > **安装容器安全服务 Agent**，在右侧弹窗中查看安装指引详情。
![](https://qcloudimg.tencent-cloud.cn/raw/a8966391675dbad4dba489b1e080e50d.png)
2.  在安装指引中，服务器类型单击选择**非腾讯云**，推荐安装方式单击选择**专线**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/67ee48c55bca284198185415f2f616a1.png" style="zoom:67%;" />
3. 如您在亚太东南（新加坡）：
 - 已有和非腾讯云机房网络互联的 VPC，则选择已连接专线的 VPC 网络，直接使用安装命令安装。
 - 没有找到相应的 VPC 网络与您的非腾讯云机房网络进行互联，可参考 [步骤2](#steps2) 云联网。

### 步骤2：确认用于连接专线的私有网络[](id:steps2)
1. 如您在当前亚太东南（新加坡）地区没有 VPC 网络，则登录 [私有网络](https://console.cloud.tencent.com/vpc/vpc?rid=1) 控制台，单击**私有网络**进入私有网络页面。
2. 在私有网络页面中，单击“下拉框”选择所需区域，单击 **+新建**，弹出新建 VPC 弹窗。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6ec8c48b834707b56627d275ed3f2fa9.png" style="zoom:67%;" />
3. 在新建 VPC 弹窗中，输入所需参数单击**确定**，即可完成新建 VPC。

### 步骤3：通过云联网实现 VPC 和已连专线的非腾讯云机房网络互通
1. 如已存在和非腾讯云机房通信的云联网，则将 [步骤2](#steps2) 中选择的 VPC 实例添加到云联网中。
   a. 登录 [私有网络](https://console.cloud.tencent.com/vpc/vpc?rid=1) 控制台，在左侧导航栏，单击**云联网**，进入云联网页面。  
   b. 在云联网页面，单击右侧**管理实例** > **关联实例**，进入关联实例页面。
   c. 在关联实例页面，单击**新增实例**，将 [步骤2](#steps2) 中选择的 VPC 实例添加到云联网中，单击**确定**即完成关联实例。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e87062c6be2c42a64397995fa57aaa58.png" style="zoom:67%;" />      
2. 如尚未配置云联网，则需要新建。
   a. 登录 [私有网络](https://console.cloud.tencent.com/vpc/vpc?rid=1) 控制台，在左侧导航栏，单击**云联网**，进入云联网页面。  
   b. 在云联网页面中，单击**+新建**，弹出新建云联网实例弹窗。
   c. 在新建云联网实例弹窗，输入所需参数单击**确定**，即可完成新建云联网实例。
>?
>- 专线网关：请选择您和非腾讯云机房通信连接的专线网关。
>- 私有网络：请选择 [步骤2](#steps2) 中选择的 VPC 实例。
>- 如出现 IP 地址段冲突，请返回 [步骤2](#steps2) 重新选择或新建一个不会冲突的 VPC 实例。   

<img src="https://qcloudimg.tencent-cloud.cn/raw/6335d335ff39ead6c4a955ceeb918ac2.png" style="zoom:67%;" />

3. 回到 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)，参考[ 步骤1 ](#steps1)获取安装命令进行安装。您的非腾讯云机房需要放通对 [步骤1](#steps1) 中描述的 IP 的5574、8080、80、9080共4个端口的访问。
