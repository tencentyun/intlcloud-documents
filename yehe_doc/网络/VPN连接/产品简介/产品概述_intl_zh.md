VPN 连接（VPN Connections）是指在 Internet 公共网络上建立的一个安全的网络连接，通过为企业提供基于公网的加密通道，从而实现将企业数据中心（IDC）、内部办公网络与腾讯云的私有网络 VPC 安全的连接起来。VPN 网关提供 IPsec  VPN 连接。

腾讯云 VPN 连接分为如下组成部分：
- VPN 网关：创建的 IPsec VPN 网关。
 - VPC 型 VPN 网关：当您需要与单个 VPC 通信时，可通过 VPC 型 VPN 网关接入 VPC。
 - CCN 型 VPN 网关：当您需要与多个 VPC 通信时，可通过 CCN 型 VPN 网关接入云联网，实现全流量互通。
>?每个 VPN 网关可以建立多个 VPN 通道，每个 VPN 通道可以打通一个本地 IDC。
>
- 对端网关：记录 IDC 端 IPsec VPN 网关公网 IP 地址的逻辑对象（IDC 端必须有固定公网 IP）。
- VPN 通道：加密的 IPsec VPN 通道。
![](https://main.qcloudimg.com/raw/b408d142266092bc5f75a8bbd659c20a.png)



