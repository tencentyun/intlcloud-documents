 ### VPN 网关是如何实现的，可用性如何？
- VPN 网关是通过网络功能虚拟化（NFV）实现的，采用双机热备的策略，单台故障时自动切换，不会影响业务正常运行。
- VPN 通道在公网中运行，公网网络出现阻塞、抖动、延迟等问题都会对 VPN 网络质量产生影响。如果业务对网络传输的延迟、抖动容忍度较低，建议使用 [专线接入](https://intl.cloud.tencent.com/document/product/216)。

### 为什么 VPN 网关与 VPN 通道显示的监控数据有时不一致？
目前 VPN 网关与 VPN 通道的数据采集位置与上报间隔存在区别，其中 VPN 网关的统计粒度为1分钟，VPN 通道的统计粒度为10秒，统计粒度不一致。因此在监控页进行数据聚合的时候，会造成 VPN 网关与 VPN 通道的展示数据不一致的情况。


### 如何配置 VPN？
IPsec VPN 可以在控制台实现全自助配置，详情请参见 [快速入门](https://intl.cloud.tencent.com/document/product/1037/32689)。

### 如何创建 VPN 网关？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 创建 VPN 网关，详情请参见 [创建 VPN 网关](https://intl.cloud.tencent.com/document/product/1037/32690)。

### 如何创建 VPN 通道？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 创建 VPN 通道，详情请参见 [创建 VPN 通道](https://intl.cloud.tencent.com/document/product/1037/32692)。

### 如何查看 VPN 连接监控数据？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 查看 VPN 连接监控数据，详情请参见[ 查看监控数据](https://intl.cloud.tencent.com/document/product/1037/32698)。

### 如何设置 VPN 连接告警？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 设置 VPN 连接告警，详情请参见 [设置告警](https://intl.cloud.tencent.com/document/product/1037/32699)。

### 如何查看 VPN 网关详细信息？
用户可以进入[私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 查看 VPN 网关详细信息，详情请参见 [查看 VPN 网关详细信息](https://intl.cloud.tencent.com/document/product/1037/32700)。

### 如何修改 VPN 通道配置？
用户可以进入 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) 修改 VPN 通道配置，详情请参见 [修改 VPN 通道配置](https://intl.cloud.tencent.com/document/product/1037/32701)。

### 如何绑定高防包？
用户可以进入 [DDoS 防护（大禹）管理控制台](https://console.cloud.tencent.com/ddos/overview) 绑定高防包，详情请参见 [绑定高防包](https://intl.cloud.tencent.com/document/product/1037/32705)。
