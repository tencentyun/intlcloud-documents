本文主要介绍单实例网络切换方案、以及迁移过程中混访处理方案。

##  单实例网络迁移
腾讯云支持基础网络内单实例一键迁移至私有网络，详情请单击以下实例链接。
<table >
<th> 实例</th>
<th> 特点</th>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/213/20278> 云服务器 CVM</a> </td>
<td> <li>需重启实例<li>基础网络IP立即变更为私有网络 IP，无保留时间</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/236/31915>云数据库 MySQL </a></td>
<td rowspan=5>在一定时间内保持双 IP 访问，原基础网络 IP 保持时间如下：<ul><li>MySQL：默认保持24小时（1天），最长可以保持168小时（7天）<li>MariaDB：保持24小时（1天）<li>TDSQL：保持24小时（1天）<li>Redis：可选择立即失效、1天后释放、2天后释放、3天后释放、或7天后释放<li>MongoDB：4.0版本以上旧IP地址立即失效，其他版本可选择立即失效、1天后释放、2天后释放、3天后释放、或7天后释放</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/237/40160>云数据库 MariaDB</a</td>
</tr>
<tr>
<td><a href=https://intl.cloud.tencent.com/document/product/1042/33340>云数据库 TDSQL</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/239/31944>云数据库 Redis</a></td>
</tr>
<td><a href=https://intl.cloud.tencent.com/document/product/240/40126>云数据库 MongoDB</a></td>
</tr>
</table>

>? 如需网络切换后云资源 IP 地址不变，可尝试创建包含基础网络 IP 的 VPC。若因客观因素无法实现时，请参考如下方案：
+ 自建内网 DNS 服务并做域名化改造，待迁移至私有网络后，可使用腾讯云 [私有域解析 Private DNS](https://intl.cloud.tencent.com/document/product/1097/40551)。
+ 使用公网IP访问。 
##  网络迁移中的混访方案
混访是指业务在网络迁移过程中支持基础网络和私有网络的混合访问。腾讯云提供如下混访方案：
+  利用云数据库在网络切换后的双 IP 访问能力，可实现云数据库实例级别的业务混访。
    ![]()
+ 对象存储 COS 的域名访问服务，使其具备混访能力。
+ 网络迁移过程中，如需网络互通，可配合如下方案实现：
  + 基础网络互通：实现基础网络内的云服务器与私有网络内的云服务器、云数据库、负载均衡等实例互通。
  + 终端连接：是对基础网络互通方案的补充，可实现私有网络内实例单向访问基础网络内的负载均衡、云数据库等非云服务器实例。
  ![]()
   >? 
   >+ 终端连接目前请 [提交工单](https://console.cloud.tencent.com/workorder/category)，且访问的资源属性依然在基础网络，不利于后期维护，建议您将资源切换至私有网络。
   >+ 如需了解更多私有网络与基础网络互通方案介绍，请参见 [与基础网络互连](https://intl.cloud.tencent.com/document/product/215/35505)；配置基础网络互通，请参见 [基础网络互通](https://intl.cloud.tencent.com/document/product/215/41418)。

