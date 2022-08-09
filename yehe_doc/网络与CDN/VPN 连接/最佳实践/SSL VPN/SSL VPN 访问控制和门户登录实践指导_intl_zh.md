本文介绍如何使用 IEAM（即数字身份管控平台）和 SSL VPN 实现访问控制，提升您业务的安全性。
>?目前 SSO 身份认证功能灰度中，当前仅支持新加坡地域，如有需要，请提交 [工单申请](https://console.cloud.tencent.com/workorder/category)。
>

## 流程
![](https://qcloudimg.tencent-cloud.cn/raw/3d9f258ad8024a35a0ab72766f30b58d.jpg)

## EIAM 认证配置
本节仅介绍 EIAM（即数字身份管控平台）认证配置的主要步骤。

### 创建用户
1. 登录 [EIAM 平台](https://console.cloud.tencent.com/eiam)，在导航栏选择**用户管理** > **组织机构管理** > **根节点**，然后在**根节点**页面单击**新建用户**。
![](https://qcloudimg.tencent-cloud.cn/raw/d0b292c8b331b8f36eb300ed3778c5b8.png)
2. 在弹出的**新建用户**页面配置相应参数。
该处用户名密码将会用于登录 [腾讯云 Client VPN 自助服务门户](https://self-service-test.vpn.woa.com/)。
![](https://qcloudimg.tencent-cloud.cn/raw/737dbcbd32db479589f1acba7a73df97.png)

### 创建用户组并添加下相应的成员
1. 在导航栏选择**用户管理** > **用户组管理**，在**用户组管理**页面单击**新建用户组**，并依据界面参数填写相应的内容，然后单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/633d6ea78a53edeb00968ba80243ed74.png)
2. 在创建好的用户组区域单击**添加用户**。
![](https://qcloudimg.tencent-cloud.cn/raw/90bc5ed0fb3975dfbede16809aa51b18.png)
3. 在弹出的**添加用户**页面将成员添加至用户组，然后单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/c912be2bb043a563af9ae0252ed06b4c.png)

### 创建 EIAM 应用
1. 在导航栏选择**应用管理**，单击**应用市场新建**，在弹出的**应用市场新建**页面选择 **腾讯云 VPN**，然后单击**下一步：编辑应用信息**。
![](https://qcloudimg.tencent-cloud.cn/raw/9c95e0f1fd5d03da1ddcddd1c840bcd8.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0e1e299ec52779d5f80eec64de78f141.png)
2. 在**编辑应用信息**页签依据界面提示填写相应的信息，然后单击**下一步：完成**。
![](https://qcloudimg.tencent-cloud.cn/raw/5b573fb2b4e2f506548a7dbe3190d4d3.png)

### EIAM 应用授权
1. 在导航栏选择**应用授权**，在**应用授权**页面单击**用户组授权**，然后单击**新增授权**。
![](https://qcloudimg.tencent-cloud.cn/raw/373558137a62501312ea50d20d23dfc7.png)
2. 在弹出的**新增授权**页面选择创建好的 EIAM 应用，然后单击**下一步：选择用户组**。
![](https://qcloudimg.tencent-cloud.cn/raw/2ca01637c87b64911cf77d810cae663a.png)
3. 在**选择用户组**页签勾选待授权的用户组，然后单击**下一步：完成**。
![](https://qcloudimg.tencent-cloud.cn/raw/04c8349c5bd5fb846de58160ad51dc47.png)


## SSL VPN 配置

### 创建 SSL VPN 网关
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)，在左侧导航栏中选择 **VPN 连接** > **VPN 网关**，进入管理页。
2. 在 VPN 网关管理页面，单击<b>+新建</b>，并在弹出的**新建 VPN 网关**页面依据界面参数配置 SSL VPN 网关。
![](https://qcloudimg.tencent-cloud.cn/raw/82738c5ab46577810286066ced03f5ae.png)
3. SSL VPN 网关参数配置完成后单击**创建**。

### 创建 SSL 服务端
1. 在左侧导航栏中选择 **VPN 连接** > **SSL 服务端**，进入管理页。
2. 在 SSL 服务端管理页面，单击<b>+新建</b>，在弹出的新建 SSL 服务端对话框中依据界面参数配置 SSL 服务端。
![](https://qcloudimg.tencent-cloud.cn/raw/516cf8533fdf72c248d80eee40b503fc.png)
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
![](https://qcloudimg.tencent-cloud.cn/raw/07420cb2280e0bd44947a8b6766fdc54.png)
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
![](https://qcloudimg.tencent-cloud.cn/raw/61410c7de573a258fa0c79a8ce5d0dea.png)

## 在 Client VPN 门户下载 SSL 客户端配置文件和 SSL 客户端
1. 登录 [腾讯云 Clinet VPN 自主服务门户](https://self-service.vpnconnection.tencent.com)。
2. 在 SSL 服务端 ID 所在行的输入框中输入创建好的 SSL 服务端 ID，然后单击**下一步**，进入登录界面。
![](https://qcloudimg.tencent-cloud.cn/raw/e62d6e75fbe70c168799a3534d86c9f3.png)
3. 登录腾讯云 Clinet VPN 自主服务门户。
 - 账户密码方式
 使用 EIAM 创建的用户密码进行登录。
 ![](https://qcloudimg.tencent-cloud.cn/raw/e94dbd40c28b390dd335de2739513369.png)
 - SAML 自动认证方式
 如果您在 EIAM 的用户组中，并在 SSL 访问控制策略中，您还可以直接单击![](https://qcloudimg.tencent-cloud.cn/raw/30a42799e4a89cef711771017807a9de.png)进行 SAML 认证，然后单击**跳转进行认证（SAML）**进行登录。
 ![](https://qcloudimg.tencent-cloud.cn/raw/69a950e698da8532368ab5d3658f2f6a.png)
4. 在**下载SSL客户端配置文件**区域找到您需要下载的客户端配置文件，单击**下载**。
![](https://qcloudimg.tencent-cloud.cn/raw/31bba25724ec755f717b7ecbd3c9aec6.png)
5. 在**下载 SSL 客户端**区域找到适合您的 SSL 客户端，单击**下载**。
本文以 MAC 为例，单击下载后跳转至 OpenVPN 官网，您可以在官网下载。
![](https://qcloudimg.tencent-cloud.cn/raw/a3acb588a5998f9f4ab26f6fae6f677e.png)

## SSL 客户端安装与连接
1. 在本地解压安装包，双击安装程序依据界面提示进行安装。
![](https://qcloudimg.tencent-cloud.cn/raw/91055f2191fa4e39f9c0b3fc283d2555.png)
2. SSL 客户端安装完成后，选择 “Import Profile” 菜单中的 “FILE” 页面，，上传已下载的 SSL 客户端配置文件（.ovpn 格式）。
![](https://qcloudimg.tencent-cloud.cn/raw/f39630923b2d06bc4b451e18a049e9a6.png)
3. 上传成功后，选择 connect 进行连接。
![](https://qcloudimg.tencent-cloud.cn/raw/2749df288279c6b7d9965b77a0621928.png)
4. Profiles 连接中，请稍候。
![](https://qcloudimg.tencent-cloud.cn/raw/41ff2524ac4ffd107059cdd00c7ac246.png)
5. 进行认证登录。
![](https://qcloudimg.tencent-cloud.cn/raw/d180678d03f8311ad6b7563a38b994d7.png)
6. 连接成功。
![](https://qcloudimg.tencent-cloud.cn/raw/3397478b0ae43da47d9c1711d60c828f.png)

