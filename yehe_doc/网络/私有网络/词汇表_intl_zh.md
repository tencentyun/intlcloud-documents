## C

### CIDR

参见 [无类别域间路由](https://intl.cloud.tencent.com/document/product/215/4925)

## E

### EIP

参见 [弹性公网 IP](https://intl.cloud.tencent.com/document/product/215/4925)

## G

### 公网 IP

公网 IP（Public IP）地址可通过 Internet 访问，并可用于实例与 Internet 之间或与其他具有公共终端节点的腾讯云资源（例如数据库资源）之间的通信。

### 公网网关

公网网关（Public Network Gateway） 是一种云服务器，具备转发 Internet 和私有网络间流量的能力，没有外网 IP 但需要进行 Internet 访问的云服务器，可通过公网网关来访问 Internet。

## J

### 基础网络

基础网络（Basic Network）是腾讯云上所有用户的公共网络资源池，该资源池内云服务器内网 IP 地址由腾讯云统一分配，配置简单，使用方便，适合对操作易用性要求比较高、需要快速使用云服务器的用户，而私有网络更适合有网络管理能力和需求的用户。
更多详情，请参见 [私有网络与基础网络](https://intl.cloud.tencent.com/document/product/215/35505)。

## K

### 可用区

指腾讯云在同一地域内电力和网络互相独立的物理数据中心。目标是能够保证可用区之间故障相互隔离，不出现故障扩散，使得用户的业务持续在线服务。

## N

### 内网 IP

内网 IP（Private IP）指在腾讯云 VPC 或基础网络内分配给实例的 IP 地址，内网 IP 地址无法通过 Internet 访问，但内网 IP 可用于 VPC 中或基础网络实例之间的通信。

## S

### 私有网络

私有网络（Virtual Private Cloud）在腾讯云构建出独立的网络空间，与您在数据中心运行的传统网络极其相似，但是托管在腾讯云私有网络内的是您在腾讯云上的服务资源，包括：[云服务器](https://intl.cloud.tencent.com/document/product/213)、[负载均衡](https://intl.cloud.tencent.com/document/product/214)、[云数据库](https://intl.cloud.tencent.com/document/product/236) 等云服务资源。您完全不用关心网络设备的采购和运维，而是通过软件自定义网段划分、IP 地址、路由策略等。您不仅可以通过 [弹性 IP](https://intl.cloud.tencent.com/document/product/213/16586) 、[NAT 网关](https://intl.cloud.tencent.com/document/product/1015) 和 [公网网关](https://intl.cloud.tencent.com/document/product/213/34835) 等灵活访问 Internet，您也可以通过 [VPN](https://intl.cloud.tencent.com/document/product/1037) / [专线接入](https://intl.cloud.tencent.com/document/product/216) 将私有网络与您的数据中心连通。同时，腾讯云私有网络的 [对等连接](https://intl.cloud.tencent.com/document/product/553) 服务可以帮助您轻松实现全球同服和两地三中心容灾。另外，腾讯云私有网络中的 安全组 和 [网络 ACL](https://intl.cloud.tencent.com/document/product/215/31850) 可以多维度、全方位的满足您的网络安全需求。

## T

### 弹性公网 IP

弹性公网 IP（Elastic IP，EIP） 是可以独立申请的公网 IP 地址，支持动态绑定和解绑。您可以将其与账户中的云服务器（或 NAT 网关实例）绑定或者解绑。主要作用是：

1. 保留 IP，因为大陆的 IP 和 DNS 之间是需要域名备案的。
2. 屏蔽实例故障，例如：动态 DNS 映射把 DNS 名称映射到 IP 地址，传播这个映射变化到整个 Internet 可能需花费24小时，而弹性 IP 实现了 IP 从一个云服务器到另一个云服务器的漂移。在任何云服务器出现故障时，只需启动另一个实例并重新映射它，从而快速响应实例故障。

## V

### VPC

参见 [私有网络](https://intl.cloud.tencent.com/document/product/215/4925)

## W

### 无类别域间路由

CIDR（Classless Inter-Domain Routing）即无类别域间路由，由您指定的独立网络空间地址块，通过 IP 和掩码结合，实现对网络的整体划分。以`10.1.0.0/16`为例，其中`10.1.0.0`为网络块的 IP，`16`为网络块的掩码。通过设定掩码的大小，可以调整网络块的大小设定。网络块包括的 IP 数 = 2 ^( 32 - 掩码)，因此`10.1.0.0/16`网络块最多包含65536个 IP 地址。