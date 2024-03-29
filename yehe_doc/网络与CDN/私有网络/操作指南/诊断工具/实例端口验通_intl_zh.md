实例端口验通功能可以帮助您检测云服务器实例的安全组端口放通情况，定位故障所在，提升使用体验。
本功能提供常用端口和自定义端口的检测，常用端口如下表所示。
 <table>
<thead>
<tr>
<th>规则类型</th>
<th>端口</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="7">入站规则</td>
<td>ICMP 协议</td>
<td>用于传递控制消息，如 ping 命令。ICMP 为控制协议，不涉及端口号。</td>
</tr>
<tr>
<td>TCP:20</td>
<td rowspan="2">用于放通 FTP 服务的上传、下载。</td>
</tr>
<tr>
<td>TCP:21</td>
</tr>
<tr>
<td>TCP:22</td>
<td>用于放通 Linux SSH 登录。</td>
</tr>
<tr>
<td>TCP:3389</td>
<td>用于放通 Windows 远程登录。</td>
</tr>
<tr>
<td>TCP:443</td>
<td>用于提供网站 HTTPS 服务。</td>
</tr>
<tr>
<td>TCP:80</td>
<td>用于提供网站 HTTP 服务。</td>
</tr>
<tr>
<td>出站规则</td>
<td>ALL</td>
<td>用于放通所有出站流量，以访问外部网络。</td>
</tr>
</tbody></table>

## 操作指南
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 单击左侧目录下方的【诊断工具】>【实例端口验通】，进入管理页面。
3. 在页面上方选择【地域】，并在列表中，找到您要验证的实例所在行，单击【一键检测】。
![](https://main.qcloudimg.com/raw/7001bc40cd91f8c17070826ba62ce0ab.png)
4. 您可以在弹窗中看到端口验通的详情，请根据实际情况选择执行如下操作。
   + 如不需要检测常用端口，可以取消勾选该条检测条目。
   + 如常用端口不满足检测要求，可在下方的自定义端口中输入需要检测的端口号，并单击【保存】。
      + 协议：可选择TCP或UDP。
      + 端口：输入需要验通的端口号，注意，端口号不可与常用端口号重复。
      + 方向：可选择入站或者出站。
      + IP：当方向为入站时，请填写输入源IP；当方向为出站时，请填写目的IP；所有来源或目的地址，请填写ALL。
      + 自定义端口检测最多支持15个。
   
 例如，除检测常用端口外，还需要自定义检测 TCP 协议、30端口，出站方向，目的 IP 为10.0.1.12的安全策略，可在自定义端口检测区域框中输入。
![](https://main.qcloudimg.com/raw/3f4067337a80ef596af55446cf5fead1.png)
5. 完成端口检查设置后，单击【开始检测】，【策略】列将展示检测结果。
![](https://main.qcloudimg.com/raw/ae7eb364c16c5bbcb52ce47615b15174.png)
<p>如果您存在某条端口策略为【未放通】，且有放通该端口的需求（例如 <b>TCP:22</b>），如下图所示。</p>

 ![](https://main.qcloudimg.com/raw/40fc364c561308d97cc1aeca54cbb1b4.png)
<p>那么，您可以在 <a href="https://console.cloud.tencent.com/vpc/securitygroup">安全组控制台</a> 进入实例绑定的安全组，添加一条放通 <b>TCP:22</b> 端口的入站规则，可根据实际需求，在【来源】中默认选择 all 放通全部 IP，或填写指定 IP（IP 段）。<p>
 
  ![](https://main.qcloudimg.com/raw/d1053c70ddce3f089737f4abf8e0c297.png)

## 相关信息
- 如需了解安全组相关内容，请参见 [安全组概述](https://intl.cloud.tencent.com/document/product/215/38750)、 [添加安全组规则](https://intl.cloud.tencent.com/document/product/215/35513)。
- 如需了解服务器常用端口相关说明，请参见 [服务器常用端口](https://intl.cloud.tencent.com/document/product/215/35520)。
