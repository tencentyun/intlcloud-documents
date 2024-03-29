负载均衡 CLB 提供四层（TCP 协议/UDP 协议/TCP SSL 协议）和七层（HTTP 协议/HTTPS 协议）负载均衡。您可以通过 CLB 将业务流量分发到多个后端服务器上，消除单点故障并保障业务可用性。CLB 自身采用集群部署，可实现会话同步，消除服务器单点，提升系统冗余，保证服务稳定，可在同一个地域部署多个机房，实现同城容灾。

## 基础架构
腾讯云负载均衡当前提供四层和七层的负载均衡服务：
- 四层主要基于腾讯自研的统一接入网关（Tencent Gateway，TGW）来实现负载均衡，TGW 具有可靠性高、扩展性强、性能高、抗攻击能力强等特点，支持 Data Plane Development Kit（DPDK）高性能转发，单集群可支持亿级并发、千万级 PPS。腾讯内部诸多业务均通过 TGW 接入服务，包括腾讯游戏、腾讯视频、微信、QQ 等。
- 七层主要基于 Secure Tencent Gateway（STGW）实现负载均衡，STGW 是腾讯基于 Nginx 自研的支持大规模并发的七层负载均衡服务，承载了腾讯内大量的七层业务流量，包括腾讯新闻、理财通、腾讯游戏、微信等。
![](https://main.qcloudimg.com/raw/c2607a45aec0366af276f70e65722f4c.png)

## 转发路径
负载均衡负责转发业务流量，由后端服务实际处理业务请求。CLB 与后端 CVM 之间是通过腾讯云内网进行通信的。TGW 和 STGW 均由多台服务器部署，通过集群来提供负载均衡服务。CLB 的转发路径如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bzmv359_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230323115443.png)
1. TCP/UDP协议：
 - TCP/UDP 协议由 TGW 集群处理转发逻辑。
 - 业务流量到达后，由 TGW 通过腾讯云内网转发给后端 CVM，后端 CVM 的回包也是通过 TGW 返回给客户端。
2. TCP SSL 协议
 - 处理 TCP SSL 协议时，业务流量会先经过 TGW 集群，而后由 STGW 集群来转发给后端 CVM。
 - 新建会话时需经过加速卡集群来进行证书的验证和加解密等前置操作。
 - 业务流量到达后，在腾讯云内网中依次通过 TGW、STGW、后端 CVM，回包也依次逆向返回给客户端。
3. HTTP/HTTPS 协议
 - 处理 HTTP/HTTPS 协议时，业务流量会先经过 TGW 集群，而后由 STGW 识别 HTTP 协议并转发给后端 CVM。
 - 新建 HTTPS 会话时需经过加速卡集群来进行证书验证和加解密等前置操作，将 HTTPS 转换成 HTTP 协议，再转发给后端 CVM。
 - 业务流量到达后，在腾讯云内网中依次通过 TGW、STGW、后端 CVM，回包也依次逆向返回给客户端。
