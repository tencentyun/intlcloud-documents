本文介绍如何使用 EIAM（即数字身份管控平台）和 SSL VPN 实现访问控制，提升您业务的安全性。
>?目前 SSO 身份认证功能灰度中，当前仅支持新加坡地域，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>

## 流程
![](https://staticintl.cloudcachetci.com/yehe/backend-news/yYKL840_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230301163656.png)	

## EIAM 认证配置
本节仅介绍 EIAM（即数字身份管控平台）认证配置的主要步骤。

### 创建用户
1. 登录 [EIAM 平台](https://console.cloud.tencent.com/eiam)，在导航栏选择**用户管理** > **组织机构管理** > **根节点**，然后在**根节点**页面单击**新建用户**。
2. 在弹出的**新建用户**页面配置相应参数。
该处用户名密码将会用于登录 [腾讯云 Client VPN 自助服务门户](https://self-service.vpnconnection.tencent.com/)。

### 创建用户组并添加下相应的成员
1. 在导航栏选择**用户管理** > **用户组管理**，在**用户组管理**页面单击**新建用户组**，并依据界面参数填写相应的内容，然后单击**确定**。
2. 在创建好的用户组区域单击**添加用户**。
3. 在弹出的**添加用户**页面将成员添加至用户组，然后单击**确定**。

### 创建 EIAM 应用
1. 在导航栏选择**应用管理**，单击**应用市场新建**，在弹出的**应用市场新建**页面选择 **腾讯云 VPN**，然后单击**下一步：编辑应用信息**。
2. 在**编辑应用信息**页签依据界面提示填写相应的信息，然后单击**下一步：完成**。

### EIAM 应用授权
1. 在导航栏选择**应用授权**，在**应用授权**页面单击**用户组授权**，然后单击**新增授权**。
2. 在弹出的**新增授权**页面选择创建好的 EIAM 应用，然后单击**下一步：选择用户组**。
3. 在**选择用户组**页签勾选待授权的用户组，然后单击**下一步：完成**。


## SSL VPN 配置

### 创建 SSL VPN 网关
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)，在左侧导航栏中选择 **VPN 连接** > **VPN 网关**，进入管理页。
2. 在 VPN 网关管理页面，单击 **+新建** ，并在弹出的**新建 VPN 网关**页面依据界面参数配置 SSL VPN 网关。
3. SSL VPN 网关参数配置完成后单击**创建**。

### 创建 SSL 服务端
1. 在左侧导航栏中选择 **VPN 连接** > **SSL 服务端**，进入管理页。
2. 在 SSL 服务端管理页面，单击 **+新建** ，在弹出的新建 SSL 服务端对话框中依据界面参数配置 SSL 服务端。
<table>
<tr>
<th>参数名称</th>
<th>参数说明</th>
</tr>
<tr>
<td>名称</td>
<td>填写 SSL 服务端名称，不超过60个字符。</td>
</tr>
<tr>
<td>地域</td>
<td>展示 SSL 服务端所在地域。</td>
</tr>
<tr>
<td>VPN 网关</td>
<td>选择创建好的 SSL VPN 网关。</td>
</tr>
<tr>
<td>本端网段</td>
<td>客户移动端访问的云上网段。</td>
</tr>
<tr>
<td>客户端网段</td>
<td>分配给用户移动端进行通信的网段，该网段请勿与腾讯侧 VPC CIDR 冲突。</td>
</tr>
<tr>
<td>协议</td>
<td>服务端传输协议。</td>
</tr>
<tr>
<td>端口</td>
<td>填写 SSL 服务端用于数据转发的端口。</td>
</tr>
<tr>
<td>认证算法</td>
<td>目前支持 SHA1 和 MD5 两种认证算法。</td>
</tr>
<tr>
<td>加密算法</td>
<td>目前支持 AES-128-CBC、AES-192-CBC 和 AES-256-CBC 加密算法。</td>
</tr>
<tr>
<td>是否压缩</td>
<td>否。</td>
</tr>
<tr>
<td>访问控制</td>
<td>选择开启。
<dx-alert infotype="explain" title="">
如果您需要使用该功能，请联系腾讯技术支持进行申请。
</dx-alert>
</td>
</tr>
<tr>
<td>认证方式</td>
<td>选择“证书认证+身份认证”。</td>
</tr>
<tr>
<td>EIAM 应用</td>
<td>选择在 EIMA 创建好的应用。</td>
</tr>
</table>

### 配置访问控制策略
1. 在左侧导航栏中选择 **VPN 连接** > **SSL 服务端**，进入管理页。
2. 在 SSL 服务端列表单击具体是实例 ID。
3. 在 SSL 服务端详情页面单击**访问控制**，并单击**新增策略**，然后依据界面信息配置策略信息。
<table>
<tr>
<th>参数名称</th>
<th>参数说明</th>
</tr>
<tr>
<td>目的端</td>
<td>填写需要本端 IP 网段，即访问云上的 IP 网段。
<dx-alert infotype="explain" title="">
目的端网段需要与本端网段在同一网段内，若更改本端网段，需主动修改访问控制的目的端地址。
</dx-alert>
</td>
</tr>
<tr>
<td>访问权限</td>
<td>选择特定的用户组，选择该项后需要配置访问组 ID。</td>
</tr>
<tr>
<td>访问组 ID</td>
<td>选择被允许访问的用户组。</td>
</tr>
<tr>
<td>备注</td>
<td>必填，填写策略的备注信息，方便您后续识别策略信息。</td>
</tr>
</table>
4. 完成配置后，单击**确定**。

### （可选）创建 SSL 客户端
>?如需[ 下载 SSL 客户端配置 ](https://intl.cloud.tencent.com/document/product/1037/43914)和连接服务端，可按需创建 SSL 客户端。
>
1. 在左侧导航栏中选择 **VPN 连接** > **SSL 客户端**，进入管理页。
2. 在**新建SSL客户端**对话框中设置客户端名称和选择待连接的 SSL 服务端，然后单击**确定**。

## 在 Client VPN 门户下载 SSL 客户端配置文件和 SSL 客户端
1. 登录 [腾讯云 Clinet VPN 自主服务门户](https://self-service.vpnconnection.tencent.com)。
2. 在 SSL 服务端 ID 所在行的输入框中输入创建好的 SSL 服务端 ID，然后单击**下一步**，进入登录界面。
3. 登录腾讯云 Clinet VPN 自主服务门户。
 使用 EIAM 创建的用户密码进行登录，本文以此为例。
4. 在**下载SSL客户端配置文件**区域找到您需要下载的客户端配置文件，单击**下载**。
5. 在**下载 SSL 客户端**区域找到适合您的 SSL 客户端，单击**下载**。
本文以 MAC 为例，单击下载后跳转至 OpenVPN 官网，您可以在官网下载。
![](https://qcloudimg.tencent-cloud.cn/raw/a3acb588a5998f9f4ab26f6fae6f677e.png)

## SSL 客户端安装与连接
1. 在本地解压安装包，双击安装程序依据界面提示进行安装。
![](https://qcloudimg.tencent-cloud.cn/raw/91055f2191fa4e39f9c0b3fc283d2555.png)
2. SSL 客户端安装完成后，选择 “Import Profile” 菜单中的 “FILE” 页面，，上传已下载的 SSL 客户端配置文件（.ovpn 格式）。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f39630923b2d06bc4b451e18a049e9a6.png" width="35%"></img>
3. 上传成功后，选择 connect 进行连接。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2749df288279c6b7d9965b77a0621928.png" width="35%">
4. Profiles 连接中，请稍候。
<img src="https://qcloudimg.tencent-cloud.cn/raw/41ff2524ac4ffd107059cdd00c7ac246.png" width="35%">
5. 进行认证登录。
<img src="https://qcloudimg.tencent-cloud.cn/raw/d180678d03f8311ad6b7563a38b994d7.png" width="35%">
6. 连接成功。
<img src="https://qcloudimg.tencent-cloud.cn/raw/3397478b0ae43da47d9c1711d60c828f.png" width="35%">
