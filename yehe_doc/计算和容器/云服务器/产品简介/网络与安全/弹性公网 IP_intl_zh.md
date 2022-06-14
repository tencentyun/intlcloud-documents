## 简介

弹性公网 IP 地址（EIP），简称弹性 IP 地址或弹性 IP。它是专为动态云计算设计的静态 IP 地址，是某地域下一个固定不变的公网 IP 地址。借助弹性公网 IP 地址，您可以快速将地址重新映射到账户中的另一个实例或 NAT 网关实例，从而屏蔽实例故障。

弹性公网 IP 未进行释放前，您可以将其一直保留于您的账号中。相较于公网 IP 仅可跟随云服务器一起申请释放，弹性公网 IP 可以与云服务器的生命周期解耦，作为云资源单独进行操作。例如，若您需要保留某个与业务强相关的公网 IP，可以将其转为弹性公网 IP 保留在您的账号中。

## EIP 和普通公网 IP 的区别
公网 IP 地址是 Internet 上的非保留地址，有公网 IP 地址的云服务器可以和 Internet 上的其他计算机互相访问。普通公网 IP 和 EIP 均为公网 IP 地址，二者均可为云资源提供访问公网和被公网访问的能力。
- 普通公网 IP：仅能在 CVM 购买时分配且无法与 CVM 解绑，如购买时未分配，则无法获得。
- EIP：可以独立购买和持有的公网 IP 地址资源，可随时与 CVM、NAT 网关、弹性网卡和高可用虚拟 IP 等云资源绑定或解绑。
>?当前普通公网 IP 仅支持常规 BGP IP 线路类型。
>
与普通公网 IP 相比， EIP 提供更灵活的管理方式，如下表所示，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/215/32382#.E5.85.AC.E7.BD.91-ipv4-.E5.9C.B0.E5.9D.80">公网 IPv4 地址</a>。
<table>
<thead>
<tr>
<th>对比项</th>
<th>普通公网 IP</th>
<th> EIP</th>
</tr>
</thead>
<tbody><tr>
<td>访问公网/被公网访问</td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>独立购买与持有</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>自由绑定与解绑</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>实时调整带宽<sup>1</sup></td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>IP 资源占用费</td>
<td>×</td>
<td>&#10003; </td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="">
[公网 IP 控制台](https://console.cloud.tencent.com/cvm/eip?rid=8) 仅支持调整 EIP 的带宽，普通公网 IP 的带宽调整请参见 [调整普通公网 IP 网络配置](https://intl.cloud.tencent.com/document/product/213/15517)。
</dx-alert>
EIP 可以与云资源的生命周期解耦合，单独进行操作。例如，若您需要保留某个与业务强相关的公网 IP 地址，可以将普通公网 IP 转换为 EIP 保留在您的账号中。


## 规则与限制

### 使用规则

- 弹性公网 IP 地址同时适用于基础网络和私有网络的实例，以及私有网络中的 [NAT 网关](https://intl.cloud.tencent.com/document/product/1015) 实例。
- 弹性 IP 地址与 CVM 实例绑定时，实例的当前公网 IP 地址会被释放。
- 销毁 CVM/NAT 网关实例，会断开与弹性 IP 地址的关联。
- 弹性公网 IP 计费规则请参考 [弹性公网 IP 计费](https://intl.cloud.tencent.com/document/product/213/17156)。
- 弹性公网 IP 操作步骤请参考 [弹性公网 IP](https://intl.cloud.tencent.com/document/product/213/16586)。

### 配额限制

| 资源 | 限制 |
|---------|:---------:|
| 每个腾讯云账户每个地域（Region）配额弹性公网 IP 个数 | 20个 |
| 每个腾讯云账户各个地域每天申购次数	 | 配额数 \* 2次 |
| 解绑 EIP 时，每个账户每天可免费重新分配公网 IP 的次数 | 10次 |

> 弹性公网 IP 配额默认不支持调整，可通过 [NAT 网关](https://intl.cloud.tencent.com/product/nat)、[负载均衡](https://intl.cloud.tencent.com/document/product/214) 进行 IP 收敛。
> - 如有特殊情况需调整，则需账号存在对应量级的云服务资源，且合理使用。
>


### 云服务器绑定公网 IP 限制


> 在2019年9月18日零点前购买的云服务器不受此限制，其支持绑定的公网 IP 数量等于您的服务器支持的 [内网 IP 数量](https://intl.cloud.tencent.com/document/product/576/18527)。
>

| 云服务器的 CPU 数 | 支持绑定的公网 IP 数量上限（含普通公网 IP 和弹性公网 IP） |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



