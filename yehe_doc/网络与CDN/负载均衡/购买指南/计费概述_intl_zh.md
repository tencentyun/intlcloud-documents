本文介绍负载均衡（CLB）的计费说明。


## 费用组成
负载均衡（CLB）的费用涉及四部分：CLB 实例费、公网网络费、跨地域绑定费、性能容量单位 LCU（Loadbalancer Capacity Unit）费。
<dx-alert infotype="explain" title="">
- LCU 费用仅在“性能容量型”负载均衡实例上收取。
- 目前腾讯云账户分为标准账户类型和传统账户类型，2020年6月17日零点后注册的账户均为标准账户类型，该时间点前注册的账户请在 <a href="https://console.cloud.tencent.com/cvm/eip">公网 IP 控制台</a> 的实例列表页面顶部查看您的账户类型。
- 若您需使用物理独占型实例，请联系您的商务经理。物理独占型实例3个月起购。
</dx-alert>
<table>
<tr>
<th>实例类型 </th>
<th>账户类型 </th>
<th>实例费 </th>
<th>公网<br/>网络费 </th>
<th>跨地域<br/>绑定费 </th>
<th>性能容量单位<br/> LCU 费</th>
</tr>
<tr>
<td rowspan="2">公网 </td>
<td >标准账户类型（原“带宽上移账户”） </td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003; </td>
<td >&#10003;</td>
</tr>
<tr>
<td >传统账户类型（原“带宽非上移账户”） </td>
<td >&#10003; </td>
<td >× </td>
<td >-</td>
<td >&#10003;</td>
</tr>
<tr>
<td >内网 </td>
<td >所有账户 </td>
<td >&#10003;</td>
<td >-</td>
<td >-</td>
<td >&#10003;</td>
</tr>
</table>

## 标准账户类型计费说明
+ 内网负载均衡免收公网网络费，收取实例费（详细说明请参见 [负载均衡实例升级调价公告](https://intl.cloud.tencent.com/zh/document/product/214/41565)）。
+ 公网负载均衡收取 CLB 实例费和公网网络费。
+ 公网负载均衡启用 <a href="https://intl.cloud.tencent.com/zh/document/product/214/38441"> 跨地域绑定2.0</a> 功能，跨域费用计算在云联网上，CLB 上不收取，如不配置，可不关注。
+ 性能容量型实例收取 LCU 费用，共享型不收取。

## 传统账户类型计费说明
+ 内网负载均衡收取实例费，不收取公网网络费（详细说明请参见 [负载均衡实例升级调价公告](https://intl.cloud.tencent.com/zh/document/product/214/41565)）。
+ 公网负载均衡仅收取实例费，公网网络请在云服务器上购买，费用请参见 [公网网络费用](https://intl.cloud.tencent.com/zh/document/product/213/39743)。
+ 传统账户类型不支持跨地域绑定功能，因此不涉及跨地域绑定费。
+ 性能容量型实例收取 LCU 费用，共享型不收取。

## 相关文档
- [标准账户类型计费说明](https://intl.cloud.tencent.com/zh/document/product/214/36998)
- [传统账户类型计费说明](https://intl.cloud.tencent.com/zh/document/product/214/8848)
