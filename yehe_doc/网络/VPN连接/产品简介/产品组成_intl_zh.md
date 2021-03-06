VPN 连接有三个组成部分：VPN 网关、对端网关、VPN 通道。
## VPN 网关
VPN 网关是 VPC 或云联网建立 VPN 连接的出口网关，与对端网关（IDC 侧的 IPsec VPN 服务网关）配合使用，主要用于腾讯云 VPC 或云联网和外部 IDC 之间建立安全可靠的加密网络通信。腾讯云 VPN 网关通过软件虚拟化处理，采用双机热备策略，单台故障时自动切换，不影响业务正常运行。

VPN 网关带宽上限分为8种：5M、10M、20M、50M、100M、200M、500M、1000M。
如果您需要 [DDoS 高防包](https://intl.cloud.tencent.com/zh/document/product/1029) 为 VPN 网关提供超大带宽的 DDoS 和 CC 防护，您可以将高防包绑定到 VPN 网关上，实现安全防护。

## 对端网关
对端网关是用来记录 IDC 端的 IPsec VPN 网关公网 IP 地址的逻辑对象（IDC 端必须有固定公网 IP），需与腾讯云 VPN 网关配合使用，一个 VPN 网关可与多个对端网关建立加密的 VPN 网络通道。

##  VPN 通道
VPN 网关和对端网关建立后，即可建立用于 VPC 或云联网与外部 IDC 之间加密通信的 VPN 通道。当前 VPN 通道支持 IPsec 加密协议，可满足绝大多数 VPN 连接的需求。
VPN 通道在运营商公网中运行，公网的网络阻塞、抖动会影响 VPN 网络质量。若业务对延时、抖动敏感，建议您通过专线接入 VPC 或云联网，更多详情，请参见 [专线接入服务](https://intl.cloud.tencent.com/product/dc)。
