IP 地址分为两类：IPv4 地址和 IPv6 地址，IPv4 应用广泛，但网络地址资源有限，IPv6 地址可以很好地解决网络地址资源有限的问题。

## IPv4 地址
腾讯云有两类 IPv4 地址：内网 IPv4 地址和公网 IPv4 地址。其中，公网 IPv4 地址又分为普通公网 IPv4 和弹性公网 IPv4，如下图所示，编号1标识（弹）表示为弹性公网 IPv4 地址、编号2标识（内）表示为内网 IPv4 地址，编号3标识（公）表示为普通公网 IPv4 地址。如果您不主动做解绑、更换等操作，内网 IPv4 和公网 IPv4 都不会改变。
>?通常如无特殊说明，内网 IP 地址、普通公网 IP 地址、弹性公网 IP 地址分别指的是内网 IPv4 地址、普通公网 IPv4 地址、弹性公网 IPv4 地址。
>
![](https://main.qcloudimg.com/raw/6bb952befc42a89392b4d2369f04820d.png)

### 内网 IPv4 地址
内网 IPv4 地址是腾讯云 IPv4 内网服务的实现形式，无法通过内网 IPv4 访问 Internet。每个云服务器实例一经创建即被分配一个内网 IPv4 地址，内网 IPv4 地址可由系统自动分配，在私有网络环境下，内网 IPv4 地址也可由用户自定义。

#### 属性
- IPv4 内网服务具有用户属性，不同用户间相互隔离，即默认无法经由 IPv4 内网访问另一个用户的云服务。
- IPv4 内网服务具有地域属性，不同地域间相互隔离，即默认无法经由 IPv4 内网访问同账户下不同地域的云服务和 VPC。

#### 适用场景
内网 IPv4 地址适用于如下场景：
- 同一私有网络或基础网络下，负载均衡与云服务器实例之间 IPv4 内网互访。
- 同一私有网络或基础网络下，云服务器实例之间 IPv4 内网互访。
- 同一私有网络或基础网络下，云服务器实例与其他云服务（如 TencentDB）之间 IPv4 内网互访。

#### 相关操作
- 获取实例的内网 IPv4 地址和设置 DNS，请参见 [获取内网 IP 地址和设置 DNS](https://intl.cloud.tencent.com/document/product/213/17941)。
- 修改私有网络中云服务器实例的内网 IPv4 地址，请参见 [修改内网 IP 地址](https://intl.cloud.tencent.com/document/product/213/16561)。

### 公网 IPv4 地址
公网 IPv4 地址分为两类：普通公网 IP 和弹性公网 IP，均可以为云服务器提供访问 IPv4 公网和被 IPv4 公网访问的能力。

#### 主要区别
普通公网 IP 和弹性公网 IP 的主要区别如下：
<table>
<thead>
<tr>
<th colspan="2" width="16%">对比项</th>
<th>普通公网 IP</th>
<th>弹性公网 IP</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2">使用场景</td>
<td>如您希望创建一个具有公网访问能力的云服务器，可以在云服务器创建时，选择由系统自动分配一个公网 IP 地址，该 IP 即为普通公网 IP，其生命周期与云服务器一致，当云服务器释放后，普通公网 IP 也随之释放。</td>
<td>如您希望长期使用某个公网 IP 地址，随业务需要绑定到指定的云服务器上，您可选择弹性公网 IP（EIP），EIP 可以反复绑定和解绑，云服务器释放后，EIP 仍然存在。</td>
</tr>
<tr>
<td colspan="2">访问公网/被公网访问能力</td>
<td colspan="2">二者作为公网 IP，访问公网和被公网访问的能力没有差别。</td>
</tr>
<tr>
<td colspan="2">获取方式</td>
<td>只能在云服务器购买时分配，如购买时未分配，则无法获得。</td>
<td><li>在控制台申请 EIP 获得。</li><li>普通公网 IP 转 EIP。</li></td>
</tr>
<tr>
<td colspan="2">特点</td>
<td>与云服务器生命周期一致，云服务器释放后，普通公网 IP 也会释放。</td>
<td><li>独立享有的 IP 资源，可随时与云服务器、NAT 网关等绑定、解绑。</li><li>不再需要时可以释放。</li></td>
</tr>
<tr>
<td colspan="2" >IP 资源费用</td>
<td>普通公网 IP 不收取 IP资源费用，仅收取公网网络费用 。</td>
<td>IP 资源费用是弹性公网 IP 费用组成的一部分，针对传统账户类型和标准账户类型，不同类型的账户收费情况不同，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/684/15246">费用组成</a>。</td>
</tr>
<tr>
<td colspan="2" rowspan="2">配额</td>
<td>IP 数无固定配额，与可购云服务器配额一致。</td>
<td>每个账户每个地域（Region）可申请：20个。</td>
</tr>
<tr>
<td colspan="2">每台云服务器绑定公网 IP（包括普通公网 IP 和 EIP）数配额请参见绑定云服务器限制。</td>
</tr>
<tr>
<td rowspan="4" >操作</td>
<td>转换 IP</td>
<td>普通公网 IP 可转换为弹性公网 IP，转换后，仅 IP 属性改变，IP 地址不变，详情请参见普通公网 IP 转 EIP。</td>
<td>弹性公网 IP 不可转换为普通公网 IP。</td>
</tr>
<tr>
<td>更换 IP</td>
<td>普通公网 IP 可以直接更换，
详情请参见 <a href="https://intl.cloud.tencent.com/document/product/213/16642" target="_blank"> 更换公网 IP 地址</a>。</td>
<td>弹性公网 IP 不可以直接更换，您可以解绑并释放后，申请新的弹性公网 IP 并绑定。</td>
</tr>
<tr>
<td>释放 IP</td>
<td>如果您不再需要该公网 IP，可在 <a href="https://console.cloud.tencent.com/cvm" target="_blank">云服务器控制台 </a>的操作栏下，选择【更多】>【IP/网卡】>【退还公网 IP】进行退还。</td>
<td>可以在弹性公网 IP 控制台释放，详情请参见释放 EIP。</td>
</tr>
<tr>
<td>找回 IP</td>
<td colspan="2">您可以找回您使用过、且未被其它用户使用的普通公网 IP/弹性公网 IP，详情请参见找回公网 IP 地址。</td>
</tr>
</tbody></table>

#### 计费说明
腾讯云对使用公网 IPv4 地址访问 IPv4 公网产生的公网网络流量，将收取公网网络费用，详情请参见[公网网络计费](https://intl.cloud.tencent.com/document/product/213/39743)。


## 相关信息
- 如需快速搭建一个 IPv4 私有网络（VPC），请参见 [快速搭建 IPv4 私有网络](https://intl.cloud.tencent.com/document/product/215/31891)。
- 如需了解弹性公网 IP 相关内容，请参见 [弹性公网 IP](https://intl.cloud.tencent.com/document/product/215/34109)。

