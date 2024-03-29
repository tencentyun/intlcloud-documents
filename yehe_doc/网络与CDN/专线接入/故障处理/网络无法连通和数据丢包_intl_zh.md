## 现象描述
部分业务出现网络无法连通，数据丢包的现象，导致业务异常。

## 可能原因
故障可能原因如下：
- [物理专线中断](#1)：物理专线损坏，例如因施工导致的线缆被误挖断。
- [带宽跑满](#2)：专用通道带宽太小，不满足业务需求。
- [安全策略配置不当](#3)：云上、云下访问来回路径不一致。
- [静态路由故障](#4)：静态路由未绑定 BFD（双向转发检测机制）导致业务访问异常。
- [BGP 路由故障](#5)：BGP 路由条目超过产品限制。
- [IP 地址冲突](#6)：云上地址空间和 VPC 地址空间重叠。

## 处理方案

<span id="1"></span>
### 物理专线中断
**单点单线模式**
用户 IDC 通过一条物理专线与一个腾讯云接入点相连，再连接至腾讯云 VPC。若专线中断时，业务直接中断。
![](https://main.qcloudimg.com/raw/59177b6fa264d350d948562a90d39309.png)
**解决方法**
收集专线线路 ID，并联系运营商报障。单点单线接入模式的专线不具备容灾能力，建议您合理规划物理线路，提升专线网络架构的稳定性和高可用性，物理线路规划请参见[ 网络规划](https://intl.cloud.tencent.com/document/product/216/38527)。

**单点双线模式**
双线单接入点模式中，用户 IDC 通过两条物理专线与一个腾讯云接入点连接，再连接至腾讯云 VPC。若某一条物理专线中断时，触发容灾。
![](https://main.qcloudimg.com/raw/424b684e55ad9f2eb059143f4682bea7.png)
**解决方法**
1. 当专线故障后，请及时通过业务监控系统确认是否业务受损。
2. 触发容灾后，请收集流量切换带来的云上、云下访问的延时和路径变化，判断备用专线是否正常使用。
3. 若备用专线不能正常使用，则通过收集的 ping 和 traceroute 测试信息来定位问题。

<span id="2"></span>
### 带宽跑满
**单点单专线模式**
用户 IDC 通过一条物理专线与一个腾讯云接入点相连，再连接至腾讯云 VPC。若专用通道带宽跑满时，则会产生丢包，导致数据丢失。
![](https://main.qcloudimg.com/raw/a4bd7f183a041965747422863e9eeb2e.png)
**解决方法**
1. 登录[ 专线接入控制台](https://console.cloud.tencent.com/dc/dc)，在“变更专用通道”页面调整带宽，具体操作请参见[ 变更通道](https://intl.cloud.tencent.com/document/product/216/19251)。
2. 若您的专用通道带宽上限已达物理专线上限，请先在业务侧进行容灾切换，然后联系专线经理扩容专线。
3. 在业务优先恢复的同时，需要对导致流量跑满原因进行溯源。

**双线双接入点模式**
用户 IDC 分别通过一条物理专线与同地域两个腾讯云接入点相连，再连接至腾讯云 VPC。
- 主备模式
若主专线的业务带宽跑满时，则会产生丢包，导致数据丢失。可以通过将两条专线的主备模式调整为负载模式，减轻线路流量压力，恢复业务数据。
![](https://main.qcloudimg.com/raw/cc8afa125dc11d04fa52513e34520069.png)
- 负载模式
若主专线和备用专线均满载，则会产生丢包，导致数据丢失。
  ![](https://main.qcloudimg.com/raw/51eca2bb50730177abda0f509323f56c.png)
**解决方法**
 1. 登录[ 专线接入控制台](https://console.cloud.tencent.com/dc/dc)，在“变更专用通道”页面调整带宽，具体操作请参见[ 变更通道](https://intl.cloud.tencent.com/document/product/216/19251)。
 2. 若您的专用通道带宽上限已达物理专线上限：
   - 主备模式：将两条专线的主备模式调整为负载模式，减轻线路流量压力，恢复业务数据。
   - 负载模式：请先在业务侧进行容灾切换，然后联系专线经理扩容专线。
 3. 在业务优先恢复的同时，需要对导致流量跑满原因进行溯源。

<span id="3"></span>
### 安全策略配置不当
用户 IDC 分别通过一条物理专线与同地域两个腾讯云接入点相连，再连接至腾讯云 VPC。若 IDC 访问腾讯云 VPC 通过主专线，腾讯云 VPC 访问 IDC 通过备专线，来回路径不一样，会导致专线流量不通。
![](https://main.qcloudimg.com/raw/8f0e2af4639de6d2db4d1ecfeffd4586.png)
**解决方法**
1. 检查主专线和备专线上是否接入了不同的安全设备（如防火墙），若接入安全设备，则需确保两个安全设备策略一致，且对双向的报文进行安全策略放行。
2. 更新安全策略后，在 IDC 的边界设备上配置 IDC 的业务 IP （该业务 IP 必须是闲置或经业务部门确认可用于测试），然后在边界设备上用该业务 IP 访问云上的业务 IP ，测试是否通信正常。
3. 若上述两个操作仍未解决您的问题，则故障可能在 IDC 内部，请自行定位排查。

<span id="4"></span>
### 静态路由故障
用户 IDC 分别通过一条物理专线与同地域两个腾讯云接入点相连，再连接至腾讯云 VPC。
若主专线串接了三层设备，当 IDC 侧设备端口异常或者三层设备到 IDC 之间的链路异常时，接入点 A 无法感知且不会触发告警。这种情况下，专用通道的静态路由仍然会发送给专线网关，因此流量仍将被转发至故障的专线上导致业务不通。
![](https://main.qcloudimg.com/raw/50f64c39bd2646138024a88faa99db26.png)
**解决方法**
建议您配置 BFD。在静态路由关联两端配置 BFD 后，会定期发送探测包，若一段时间内没有收到对端发送的回复，则判定对端故障，与之关联的路由随之失效且不会转发至专线网关。

具体步骤：[提工单 ](https://console.cloud.tencent.com/workorder/category)申请开启专用通道 BFD 功能，腾讯云后台将下发配置。
 > ? 腾讯云默认的 BFD 为动态 BFD，本端 TX Interval 等于 MAX（本端 Desired Min TX Interval，对端 Required Min RX Interval）。
 >- 若专用通道为1.0 版本：
 >  - 若在2019年10月1日之前申请，Desired Min TX Interval 和 Required Min RX Interval 均为100ms，Detect Mult 为 3。
>   - 若在2019年10月1日及以后申请，Desired Min TX Interval 和 Required Min RX Interval 均为300ms，Detect Mult 为 3。
>- 若专用通道为2.0 版本：
>  - Desired Min TX Interval 和 Required Min RX Interval 最小为1000ms，Detect Mult 为 3。
>  

<span id="5"></span>
### BGP 路由故障
每条专用通道可接受的 BGP 路由条目数为100条，超过的路由将不会被接受，导致业务故障。
**解决方法**
请合理规划网络地址，进行 CIDR 子网合并，减少 IDC 发往腾讯云 VPC 的路由条目数。

<span id="6"></span>
### IP 地址冲突
云上 VPC 和云下 IDC 均遵循 TCP/IP 协议的网络空间，基于目的 IP 进行三层寻址，基于目的 MAC 进行二层寻址。因此，在混合云场景中，可能因为云上地址空间和 VPC 地址空间重叠导致 IP 地址冲突、业务访问受限的问题。
**解决方法**
1. 进行合理的网络规划。
	1. 将腾讯云 VPC 和本地 IDC 的地址进行统一规划。
	2. 将互联 IP 等网络地址进行全局统一规划。
2. 若业务场景不允许进行网络拆分再规划，可以使用 NAT 型的专线网关，实现 VPC 的地址进行本端地址转换和 IDC 的对端地址转换功能，进而实现 VPC 和 IDC 两端地址的彼此隐藏。具体操作请参见[ 配置网络地址转换（NAT）](https://intl.cloud.tencent.com/document/product/216/19257)。
>? 每个 NAT 型的专线网关本端 IP 转换和对端 IP 转换规则数量分别都是100条。
