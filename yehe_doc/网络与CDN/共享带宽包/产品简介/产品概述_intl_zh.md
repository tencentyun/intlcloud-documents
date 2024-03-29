共享带宽包（BWP）是一种多 IP 聚合的计费模式，可大幅降低公网费用。当业务中公网流量高峰分布在不同时间段内，可通过共享带宽包实现带宽聚合计费，相比单独为每台设备购买带宽，可帮您节省带宽费用。
共享带宽包提供 [月 TOP5 计费](https://intl.cloud.tencent.com/zh/document/product/684/15255)，[月95计费](https://intl.cloud.tencent.com/zh/document/product/684/15255) 两种计费模式 ，满足您不同业务场景。
>? 目前共享带宽包处于内测阶段，如需使用，请提交内测申请。
>

## 产品类别
共享带宽包按照网络计费所属主体可以分为 IP 带宽包和设备带宽包。
- **IP 带宽包**：是针对公网费用在公网 IP 或 CLB 上结算的账户，即创建 IP 或 CLB 实例时指定公网能力（带宽上限）、计费方式（按流量计费、按带宽计费）的账户，此类带宽包统称为 “IP 带宽包”。
- **设备带宽包**：是针对公网费用在设备上结算的账户，即创建 CVM 实例时指定实例的公网能力（带宽上限）、计费方式（按流量计费、按带宽计费），公网 IP 和 CLB 只作为公网出口。 此类带宽包统称为 “设备带宽包”。

腾讯云有两类账户，两类账户分别支持不同类型的带宽包：
<table>
<tr>
<th>账户类型</th><th>支持的带宽包类型</th>
</tr>
<tr>
<td rowspan="2">传统账户类型</td><td>设备带宽包</td>
</tr>
<tr>
<td>IP 带宽包（仅弹性公网 IPv6、IPv6 负载均衡和弹性公网 IP中的静态单线 IP 支持）</td>
</tr>
<tr>
<td>标准账户类型</td><td>IP 带宽包</td>
</tr>
</table>

如需确认您的账户类型，请参见 [判断账户类型](https://intl.cloud.tencent.com/document/product/684/15246)。
>?传统账户类型可以提交 [工单申请](https://console.cloud.tencent.com/workorder/category)，升级为标准账户类型；但标准账户类型无法降级为传统账户类型。
>

## 支持资源 
- 设备带宽包支持的资源类型：云服务器、负载均衡。
- IP 带宽包支持的资源类型：普通公网 IP、弹性公网 IP（支持绑定云服务器、NAT 网关）、弹性公网 IPv6、负载均衡。
