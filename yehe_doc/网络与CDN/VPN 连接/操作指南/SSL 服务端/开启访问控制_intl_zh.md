为了确保您的业务的安全性，SSL VPN 提供了SSL 服务端访问控制功能，让您的链路安全性更高。

## 注意事项
- 开启访问控制后，在服务端创建完成之后您需要配置对应访问策略，否则服务端将拒绝所有连接。
- 如果认证方式仅选择了**证书认证**，默认该 SSL 服务端将接受所有连接。
>?目前只有支持 SSO 身份认证 SSL VPN 支持访问控制功能，详情见 [SSO 认证](https://intl.cloud.tencent.com/document/product/1037/48813)。
>

## 在创建 SSL 服务端时开启访问控制
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧目录中单击 **VPN 连接** > **SSL 服务端**，进入管理页面。
3. 在 SSL 服务端管理页面，单击<b>+新建</b>。
4. 在弹出的**新建 SSL 服务端**对话框中，开启身份认证时同步开启访问控制并配置相关参数。
>?如您开启访问控制，在服务端创建完成之后您需要[ 配置访问控制策略](https://intl.cloud.tencent.com/document/product/1037/48816)，否则服务端将拒绝所有连接。
>
![](https://qcloudimg.tencent-cloud.cn/raw/0f6f3db8d4fd7df53802dbd5b5335ee2.png)
<table>
<tr>
<th>参数名称</th>
<th>参数说明</th>
</tr>
<tr>
<td>认证方式</td>
<td><ul><li>证书认证：该认证方式默认 SSL 服务端可被 SSL 客户端全量访问。</li><li>证书认证 + 身份认证：该认证方式仅允许在控制策略中的访问策略连接，您可选择为特定用户组或全部用户配置访问策略，勾选后需要选择对应的 EIAM 应用。</li></ul></td>
</tr>
<tr>
<td>EIAM 应用</td>
<td>EIAM 是在<a href="https://console.cloud.tencent.com/eiam"> 数字身份管控平台 </a>所创建的用于访问控制的应用。</td>
</tr>
<tr>
<td>访问控制</td>
<td>SSL 服务端访问控制开关。</td>
</tr>
</table>


## 在创建 SSL 服务端后开启访问控制
>?如您开启访问控制，在服务端创建完成之后您需要配置对应访问策略，否则服务端将拒绝所有连接。
>
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧目录中单击 **VPN 连接** > **SSL 服务端**，进入管理页面。
3. 在 SSL 服务端管理页面，单击具体的实例名称。
4. 在实例详情页的**基本信息**页签的服务端配置开启认证策略。
![](https://qcloudimg.tencent-cloud.cn/raw/d8178e07dc5d9310511bd218772a3fbb.png)
