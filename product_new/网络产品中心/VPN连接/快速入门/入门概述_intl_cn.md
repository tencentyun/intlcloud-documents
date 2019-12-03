您需要完成几个步骤使 VPN 连接生效，之后可以在控制台实现  IPsec VPN 全自助配置，下文将为您举例说明。
## 示例
通过 IPsec VPN 连接，打通您在**广州**的私有网络 TomVPC 中的子网 A：`192.168.1.0/24`与您 IDC 中的子网：`10.0.1.0/24`，而您 IDC 中 VPN 网关的公网 IP 是`202.108.22.5`。
![](https://main.qcloudimg.com/raw/a0ad82287cdaf9fae922e0c59fed99ba.png)
## 步骤说明
VPN 连接激活流程图如下所示：
![](https://main.qcloudimg.com/raw/8f017e7278462b27bf2aae995e6c280a.png)
具体操作请参见：
- [步骤 1： 创建 VPN 网关](https://intl.cloud.tencent.com/document/product/1037/32690)
- [步骤 2：创建对端网关](https://intl.cloud.tencent.com/document/product/1037/32691)
- [步骤 3：创建 VPN 通道](https://intl.cloud.tencent.com/document/product/1037/32692)
- [步骤 4：本地网关配置](https://intl.cloud.tencent.com/document/product/1037/32693)
- [步骤 5：配置路由表](https://intl.cloud.tencent.com/document/product/1037/32694)
- [步骤 6：激活 VPN 隧道](https://intl.cloud.tencent.com/document/product/1037/32695)
