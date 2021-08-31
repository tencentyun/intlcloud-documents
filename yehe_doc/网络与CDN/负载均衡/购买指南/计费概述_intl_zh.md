## 费用组成
负载均衡（CLB）的费用由两部分组成：实例费、公网网络费。

 <table>
 <tr>
 <th>实例类型 </th>
 <th>账户类型 </th>
 <th>实例费 </th>
 <th>公网网络费 </th>
 <th>说明 </th>
 </tr>
 <tr>
 <td rowspan="2">公网 </td>
 <td >非带宽上移账户 </td>
 <td >&#10003; </td>
 <td >× </td>
 <td > <li>在 CLB 上收取实例费。</li> <li>
在 CVM 上收取公网网络费，CLB 上没有公网网络费。 </li> <li>更多信息，请参见 <a href="https://intl.cloud.tencent.com/document/product/214/8848">非带宽上移账户计费说明</a>。</li></td>
 </tr>
 <tr>
 <td >带宽上移账户 </td>
 <td >&#10003; </td>
 <td >&#10003; </td>
 <td ><li>在 CLB 上收取实例费和公网网络费。 </li>  <li>更多信息，请参见<a href="https://intl.cloud.tencent.com/document/product/214/36998"> 带宽上移账户计费说明</a>。</li> </td>
 </tr>
 <tr>
 <td >内网 </td>
 <td >所有账户 </td>
 <td >—</td>
 <td >— </td>
 <td >内网不收取费用。</td>
 </tr>
 </table>

## 账户类型
>? 
> - 2020年6月17日后注册的腾讯云账户均为带宽上移账户。对于2020年6月17日前注册的腾讯云账户，请在控制台查看您的账户类型，具体操作请参见 [账户类型区分](https://intl.cloud.tencent.com/document/product/684/15246)。
> - 带宽上移是账户维度的属性，一个账户只能是带宽上移或者非带宽上移；不支持部分资源带宽上移、部分资源非带宽上移。

### 非带宽上移账户
- 非带宽上移账户指公网网络费用在云服务器上结算，负载均衡仅作为公网出口，即创建 CVM 实例时指定公网计费模式和带宽上限，创建公网 CLB 时没有网络计费相关配置。
- 非带宽上移账户在公网 CLB 的购买页和列表页中，均没有公网带宽信息：
 - **购买页**
![](https://main.qcloudimg.com/raw/002bfe22170790f2bebaa2840f274e3d.png)
 - **列表页**
![](https://main.qcloudimg.com/raw/14521f3afe27876f866419c29168915d.png)

### 带宽上移账户
- 带宽上移账户指将公网网络计费从云服务器上移到公网 IP 或 CLB 上，在公网 IP 或 CLB 上指定公网计费模式和带宽上限。
- 带宽上移账户在公网 CLB 的购买页和列表页，均有公网带宽信息：
 - **购买页**
![](https://main.qcloudimg.com/raw/48da1dad2b1cc02a0c0165f0155d28a3.png)
 - **列表页**
![](https://main.qcloudimg.com/raw/ae9f890d5c71a28920deed8cb0dfd536.png)

