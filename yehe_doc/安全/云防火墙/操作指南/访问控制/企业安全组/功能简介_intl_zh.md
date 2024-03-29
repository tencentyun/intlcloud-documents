企业安全组是一种全新的安全组控制平面，可以取代云服务器控制台的安全组管理界面。对安全组的配置逻辑进行了重新设计，维护了统一的访问控制管理页面，极大优化了安全组的使用体验。云防火墙提供基于五元组的规则配置界面，并通过智能转换算法自动下发安全组策略，大幅简化了安全组的配置操作。
![](https://qcloudimg.tencent-cloud.cn/raw/9c7dcade591d0cec16ea8246f39b25f9.jpg)

## 企业安全组特点
-	大幅简化了安全组的配置操作，并保留五元组规则的使用习惯。
-	更加方便的支持 VPC 间、子网间及专线接入的访问控制。
- 提供安全组的访问控制日志，方便回溯阻断情况和日常排障。
-	无需改变网络架构，对网络稳定性没有任何影响，在网络性能方面也不产生额外的瓶颈。

## 企业安全组限制
企业安全组基于云服务器安全组的底层架构进行开发，所以受限于安全组的底层功能实现和资源配额。

## 企业安全组规则
### 规则的组成部分
- 访问源和访问目的：根据入站或出站的方向不同，可以是 IP 地址、CIDR 地址块、实例、子网或私有网络。
- 目的端口：目的端口号。当协议类型为 ICMP 或 ANY 时，此项无需配置。
- 协议类型：	目前支持 TCP、UDP 和 ICMP。ANY 代表全部已支持的协议。
- 策略：规则命中后，所执行的操作。
	- 放行策略，放行命中规则的流量，不记录访问控制日志。
	- 阻断策略，拦截命中规则的流量，记录访问控制日志。

### 规则的优先级
安全组规则具有优先级，规则优先级通过规则在列表中的位置来表示，列表顶端规则优先级最高，列表底端规则优先级最低。
执行顺序是从高优先级向低优先级进行逐条匹配，规则命中后，则不再匹配后续规则。
入站规则和出站规则，分属不同的规则列表，优先级互不影响。

## 自动双向下发
为了提高安全组的配置效率，企业安全组提供了“自动双向下发”功能。在内网对内网的双向阻断或放行的场景中，不再需要在两个方向配置两条一模一样的规则。使用这个功能可以自动实现这种操作，降低规则配置的工作量。

当访问源地址填写为实例、子网或私有网络地址时，可通过“自动双向下发”功能，自动配置一条相同的出站规则（执行顺序为最高）。
>!只适用于内网到内网的通信场景。

例如，假设有两个实例，实例1的 IP 为 IP1，实例2的 IP 为 IP2。
用户对实例1和实例2分别配置了 deny all 的安全组，此时想要对实例1到实例2的访问做单向放行，需要手动配置两条安全组规则：
- 实例1，出站方向对 IP2 放行。
- 实例2，入站方向对 IP1 放行。


## 日志
### 安全组阻断日志
[安全组阻断日志](https://console.cloud.tencent.com/cfw/log/secgroup) 可展示所有企业安全组阻断策略生效的情况，目前仅支持 [少量机型](https://intl.cloud.tencent.com/document/product/682/18934)。

### 企业安全组操作日志
[企业安全组操作日志](https://console.cloud.tencent.com/cfw/operatelog/safe) 用于记录某个账号在企业安全组页面中进行的操作。

