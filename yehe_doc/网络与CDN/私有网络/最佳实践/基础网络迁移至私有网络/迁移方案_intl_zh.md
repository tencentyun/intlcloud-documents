本文主要介绍 [基础网络](https://intl.cloud.tencent.com/document/product/215/41417) 迁移到 [私有网络](https://intl.cloud.tencent.com/document/product/215/535) 的网络切换方案。

>? 
> 网络切换前，需提前创建好与待迁移基础网络实例同地域的私有网络，以及同可用区的子网，具体请参见 [ 创建私有网络](https://intl.cloud.tencent.com/document/product/215/31805)。

目前腾讯云提供两种方案，两种方案可独立使用，也可结合实际业务迁移场景组合使用：
+ 单实例网络迁移：如果您仅持有云服务器、云数据库其中一个实例，或您可接受实例单独迁移，可采用此方案。
+ 混访方案：当您的业务比较复杂，例如同时包含 CVM、CLB 及云数据库时，为了保证业务平滑迁移，可使用该方案。

##  单实例网络迁移
腾讯云支持基础网络内单实例一键迁移至私有网络，详情请单击以下实例链接。
<table >
<tr>
<th width="25%">实例</th>
<th>特点</th>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278> 云服务器 CVM</a> </td>
<td> <ul><li>需重启实例</li><li>基础网络IP立即变更为私有网络 IP，无保留时间</li><li>如云服务器有公网 IP，网络切换后公网 IP 地址不变，不会影响域名访问</li></ul></td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>云数据库 MySQL </a></td>
<td rowspan=5>在一定时间内保持双 IP 访问，原基础网络 IP 保持时间如下：<ul><li>MySQL：默认保持24小时（1天），最长可以保持168小时（7天）<li>MariaDB：保持24小时（1天）<li>TDSQL：保持24小时（1天）<li>Redis：可选择立即失效、1天后释放、2天后释放、3天后释放、或7天后释放<li>MongoDB：4.0版本以上旧 IP 地址立即失效，其他版本可选择立即失效、1天后释放、2天后释放、3天后释放、或7天后释放</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>云数据库 MariaDB</a</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>云数据库 TDSQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>云数据库 Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/44180>云数据库 MongoDB</a></td>
</tr>
<tr>
<td><a href=> 云数据库 PostgreSQL</a> </td>
<td>一个实例最多同时存在两套网络配置，且两套网络可同时进行业务访问，不同网络的 IP 可以相同</td>
</tr>
</table>

>?如需网络切换后云资源 IP 地址不变，可尝试创建包含基础网络 IP 的 VPC。若因客观因素无法实现时，请参考如下方案：
>+ 自建内网 DNS 服务并做域名化改造，待迁移至私有网络后，可使用腾讯云 [私有域解析 Private DNS](https://intl.cloud.tencent.com/document/product/1097/40551)。
>+ 使用公网 IP 访问。 

##  网络迁移中的混访方案
混访是指业务在网络迁移过程中支持基础网络和私有网络的混合访问。腾讯云提供如下混访方案：
+  云数据库：网络切换后可保持双 IP 访问，可实现云数据库实例级别的业务混访。
    ![]()
+ 对象存储 COS： 域名访问服务，天然具备混访能力。
+ 云服务器：
  + 基础网络互通：实现基础网络内的云服务器与私有网络内的云服务器、云数据库、负载均衡等实例互通。
  + 终端连接：是对基础网络互通方案的补充，可实现私有网络内实例单向访问基础网络内的负载均衡、云数据库等非云服务器实例。
![]()
>?
>+ 终端连接如需使用，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 。由于终端连接中访问的资源属性依然在基础网络，不利于后期维护，建议您将资源切换至私有网F络。
>+ 配置基础网络互通，请参见 [基础网络互通](https://intl.cloud.tencent.com/document/product/215/31807)。
>+ 如涉及 CLB 业务，为使业务平滑迁移，可参见[公网 CLB 网络切换示例](https://intl.cloud.tencent.com/document/product/215/41415)、[内网 CLB 业务迁移中的混访示例](https://intl.cloud.tencent.com/document/product/215/41416)。
