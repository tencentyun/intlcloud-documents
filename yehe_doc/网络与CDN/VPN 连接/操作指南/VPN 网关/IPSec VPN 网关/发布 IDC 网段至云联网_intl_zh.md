如果您需要打通 VPN 和云联网 CCN，可以发布网段至 CCN。
>?如果 VPN 通道的通信模式为“目的路由”，那么不需要发布 IDC 网段至云联网。
>

## 前提条件
- 已 [创建 CCN 型 IPsec VPN 网关 ](https://intl.cloud.tencent.com/document/product/1037/39688)且已 [绑定云联网实例](https://intl.cloud.tencent.com/document/product/1037/46429)。
- 已在 [VPN 通道配置 SPD 策略](https://intl.cloud.tencent.com/document/product/1037/39635)。

## 操作步骤
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 在左侧目录中单击 **VPN 连接** > **VPN 网关**，进入管理页。
3. 单击需要查看的 VPN 网关 ID，进入 VPN 网关详情页。
![]()
4. 在详情页面的**发布网段**页签发布云联网方向的网段。
![]()
该处网段为 VPN 通道创建配置 SPD 策略时对端网关的网段。