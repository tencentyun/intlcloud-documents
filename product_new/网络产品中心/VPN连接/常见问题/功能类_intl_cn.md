 ### VPN 网关是如何实现的，可用性如何？
- VPN 网关是通过网络功能虚拟化（NFV）实现的，采用双机热备的策略，单台故障时自动切换，不会影响业务正常运行。
- VPN 通道在公网中运行，公网网络出现阻塞、抖动、延迟等问题都会对 VPN 网络质量产生影响。如果业务对网络传输的延迟、抖动容忍度较低，建议使用 专线接入 。

### 是否支持 SSL-VPN？

不支持。目前仅支持 IPsec VPN，如需使用 SSL-VPN，推荐您购买云市场 [SSL-VPN](https://market.cloud.tencent.com/search/SSLVPN) 产品。

### VPN 通道未连通如何处理？

VPN 通道连通的配置过程需要两端协商信息一致才可成功建立连接，需要依次检查两端配置的一致性，推荐的检查思路如下：
>
>- 任何一个参数不一致，VPN 通道都无法建立。
>- 不同厂家设备、公有云服务提供商的默认 VPN 配置不尽相同。

1. 检查第一阶段 IKE 配置信息
请您检查第一阶段所需的 IKE 版本号、身份证认证方法、加密算法、认证算法、协商模式、两端标识、DH group、IKE sa lifetime 两端的所有参数是否保持一致，如果有不一致的请修改一致后再尝试。
腾讯云 VPN 网关的第一阶段协商参数的默认配置为：
<table><tbody>
<tr><th>IKE 配置项</th><th>默认配置</th><th>其他可选配置</th></tr>
<tr><td>IKE</td><td>V1</td><td>-</td></tr>
<tr><td>身份认证方法</td><td>预共享密钥</td><td>AES-128，AES-192，AES-256，DES</td></tr>
<tr><td>加密算法</td><td>3DES</td><td>SHA1</td></tr>
<tr><td>认证算法</td><td>MD5</td><td>-</td></tr>
<tr><td>协商模式</td><td>Main</td><td>Aggressive</td></tr>
<tr><td>本端标识</td><td>IP 地址（默认为腾讯云侧 VPN 网关的公网 IP 地址）</td><td>FQDN</td></tr>
<tr><td>对端标识</td><td> IP 地址（默认为对端 VPN 网关的公网 IP 地址）</td><td>FQDN</td></tr>
<tr><td>DH group</td><td>DH1</td><td>DH2，DH5，DH14，DH24</td></tr>
<tr><td>IKE SA Lifetime</td><td>86400秒 </td><td>-</td></tr>
</tbody></table>
2. 检查第二阶段 IKE 配置信息
请您检查第二阶段的所需的加密算法、认证方法、报文封装模式、安全协议、PFS、Ipsec SA 生成周期两端的所有参数是否一致，如果有不一致的请修改一致后再尝试。
腾讯云 VPN 网关的第二阶段 IPsec 参数的默认配置为：
<table><tbody>
<tr><th>IPsec 配置项</th><th>默认配置</th><th>其他可选配置</th></tr>
<tr><td>加密算法</td><td>3DES</td><td>AES-128，AES-192，AES-256，DES</td></tr>
<tr><td>认证算法</td><td>MD5</td><td>SHA1</td></tr>
<tr><td>PFS</td><td>Disable</td><td>DH1，DH2，DH5，DH14，DH24</td></tr>
<tr><td>Ipsec SA lifetime</td><td>3600秒</td><td>-</td></tr>
</tbody></table>
