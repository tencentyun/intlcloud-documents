## A

### 安全组

安全组（Security Group）是一种有状态的包过滤功能的虚拟防火墙，它用于设置单台或多台云服务器的网络访问控制，可以将同一地域内具有相同网络安全隔离需求的云服务器实例加到同一个安全组内，通过安全组的网络策略对云服务器的出入流量进行安全过滤。

## C

### CLB

参见 [负载均衡](#clb)

## D

### 地域

地域（Region） 是腾讯云托管机房分布地区，地域下有不同的可用区。
例如：一个托管机房的地域是北京，可用区是北京一区。处于同一地域的云服务产品可以通过内网互通，不同地域云产品之间内网不互通，选择最靠近您客户的地域，可降低访问时延、提高下载速度。

## F
<span id="clb"></span>
### 负载均衡

负载均衡（CloudLoadBalancer，CLB）是腾讯云提供的一种安全、稳定、可弹性扩展的流量分发服务，通过消除单点故障来提高系统可用性。

### 负载均衡监听器

负载均衡监听器（Load Balance Listener）提供了请求分发的规则，包括监听端口、负载均衡策略和健康检查配置等，请求会按负载均衡监听器的配置转发到后端服务器上。一个负载均衡实例请至少添加一个监听器。

### 负载均衡实例

负载均衡实例（CloudLoadBalancer Instance）是一个运行的负载均衡服务，如需使用负载均衡，须先创建一个负载均衡实例。

## H
<span id="RS"></span>
### 后端服务器

后端服务器（Real Server，RS）是一组 CVM（云服务器）实例，用于处理负载均衡分发的请求。

## R

### RS

参见 [后端服务器](#RS)

## S
<span id="vpc"></span>
### 私有网络

私有网络（Virtual Private Cloud）在腾讯云构建出独立的网络空间，与您在数据中心运行的传统网络极其相似，但是托管在腾讯云私有网络内的是您在腾讯云上的服务资源，包括：[云服务器](https://intl.cloud.tencent.com/document/product/213)、[负载均衡](https://intl.cloud.tencent.com/document/product/214)、[云数据库](https://intl.cloud.tencent.com/document/product/236) 等云服务资源。您完全不用关心网络设备的采购和运维，而是通过软件自定义网段划分、IP 地址、路由策略等。您不仅可以通过 [弹性 IP](https://intl.cloud.tencent.com/document/product/213/16586) 、[NAT 网关](https://intl.cloud.tencent.com/document/product/1015) 和 [公网网关](https://intl.cloud.tencent.com/document/product/213/34835) 等灵活访问 Internet，您也可以通过 [VPN](https://intl.cloud.tencent.com/document/product/215) / [专线接入](https://intl.cloud.tencent.com/document/product/216) 将私有网络与您的数据中心连通。同时，腾讯云私有网络的 [对等连接](https://intl.cloud.tencent.com/document/product/553) 服务可以帮助您轻松实现全球同服和两地三中心容灾。另外，腾讯云私有网络中的安全组 和 [网络 ACL](https://intl.cloud.tencent.com/document/product/215/31850) 可以多维度、全方位的满足您的网络安全需求。

## V

### VIP

参见 [虚拟服务地址](#vip)

### VPC

参见 [私有网络](#vpc)

## X
<span id="vip"></span>
### 虚拟服务地址

虚拟服务地址（virtual IP，VIP）是系统为负载均衡实例分配的服务 IP 地址。用户可以选择该服务地址是否对外网公开，可分别创建公网和内网类型的负载均衡实例。您可以将域名解析到公网 VIP 来提供对外服务。