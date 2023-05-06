本教程将帮助您快速搭建一个具有 IPv4 CIDR 的私有网络（VPC）。
## 操作场景
帮助您快速搭建一个具有 IPv4 CIDR 的私有网络（VPC），提供从新建私有网络和子网，到云服务器的购买并绑定一个弹性公网 IP（EIP），并最终实现公网访问的全程指导。
![](https://qcloudimg.tencent-cloud.cn/raw/926843feffd998e8dbf151b63178b366.png)

## 前提条件
在开始使用腾讯云产品前，您需要先 [注册腾讯云账号](https://www.tencentcloud.com/account/register) ，并完成 [实名认证](https://www.tencentcloud.com/document/product/378/3629)。

## 操作步骤
### 步骤一：创建私有网络与子网
>?私有网络和子网的 CIDR（即网段）一旦创建则无法修改，请提前做好 [网络规划](https://intl.cloud.tencent.com/document/product/215/31795)。
>
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在顶部选择私有网络所属的地域后，单击**+新建**。
3. 在**新建 VPC** 弹窗中，根据如下信息配置私有网络信息和初始子网，然后单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/ba0387f51ed8112ab819d5cb9c5113b5.png)
 - **私有网络信息**
    -  名称：私有网络名称。
    -  IPv4 CIDR：您可选择如下任意一个网段作为私有网络网段，如10.0.0.0/16。
      - 10.0.0.0 - 10.255.255.255（掩码范围需在12 - 28之间）
      - 172.16.0.0 - 172.31.255.255（掩码范围需在12 - 28之间）
      - 192.168.0.0 - 192.168.255.255 （掩码范围需在16 - 28之间）
     - 标签：您可按需添加标签，帮助您更好地管理子用户、协作者的资源权限。
  - **初始子网信息**
    -  IPv4 CIDR：
		- 您可选择在私有网络网段范围内或与私有网络的网段相同的网段，如私有网络网段为 10.0.0.0/16，则您可选择10.0.0.0/16-10.0.0.248/29之间的网段作为子网网段。
		- 如果子网所属私有网络与其他私有网络或 IDC 有通信需求，请避免子网网段与对端网段重叠，网段重叠则无法内网互通。
    - 可用区：选择子网的可用区。同一私有网络下可有不同可用区的子网，同一私有网络下不同可用区的子网默认内网互通。
    - 标签：您可按需添加标签，帮助您更好地管理子用户、协作者的资源权限。

### 步骤二：购买云服务器
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm)，在已创建的私有网络中创建一个云服务器实例。
2. 单击列表页左上方的**新建**，进入[ 云服务器购买页](https://buy.intl.cloud.tencent.com/cvm?tab=custom)。
3. 在自定义配置页面，配置云服务器实例，完成后单击**立即购买**。本操作中云服务器的网络配置如下：
 - 网络：选择已创建的私有网络和子网。
![](https://qcloudimg.tencent-cloud.cn/raw/7ec59dbff60a37870ef4f9cdaf2aff70.png)
 - 公网带宽：不勾选<img src="https://main.qcloudimg.com/raw/50eef42428eb34dc35cf40995c9b7736.png" style="margin:-3px 0">。
![](https://qcloudimg.tencent-cloud.cn/raw/f59fd4da95bd18e3f8585a1541d7547b.png)
 - 安全组：选择新建安全组，配置建议请参见 [配置安全组](https://intl.cloud.tencent.com/document/product/213/15377)。
![](https://qcloudimg.tencent-cloud.cn/raw/72584971b62015e38c9ad22da7ddd3d4.png)

### 步骤三：申请 EIP 并绑定云服务器
申请弹性公网 IP（即 EIP，可以独立购买和持有的 IP 资源），并将 EIP 绑定到云服务器实例，以实现公网访问。
1. 登录 [EIP 控制台](https://console.cloud.tencent.com/cvm/eip)。
2. 在 EIP 管理页面，选择已创建的云服务器所在地域，单击**申请**。
3. 在弹出的 “申请 EIP” 窗口中，配置相关参数，然后单击**确定**，完成 EIP 的申请。
4. 在 EIP 管理页面，找到已申请的 EIP，单击**更多** > **绑定**。
5. 在弹出的“绑定资源”窗口中，选择**CVM 实例**为绑定资源类型，再选择已创建的云服务器，单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/s36E860_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406180609.png)
6. 在弹出的提示框中，单击**确定**，即可完成与云服务器的绑定。


### 步骤四：测试公网连通性
完成如下操作，测试云服务器实例的公网连通性。
>?测试前，请确保安全组已允许对应 IP /端口访问，例如，放通 ICMP 协议，允许公网 Ping 服务器，您可通过 [查看安全组规则](https://intl.cloud.tencent.com/document/product/215/35514) 进行确认。
>
1. 登录已绑定 EIP 的云服务器实例，具体操作请参见 [登录及远程连接](https://www.tencentcloud.com/document/product/213/17278)。
2. 执行`ping 其它公网地址` ，如 `ping www.qq.com` 测试公网连通性。
![](https://main.qcloudimg.com/raw/e19b0921e6d0471ca0e9b78923ccdd06.png)


