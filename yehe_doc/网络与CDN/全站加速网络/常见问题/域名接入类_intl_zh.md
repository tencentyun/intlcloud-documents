### 如何将域名接入 ECDN 加速平台？

域名接入 ECDN 全站加速平台仅需要执行三步操作：
1. 控制台新增加速域名配置。
2. 设置 HOST 验证配置生效。
3. 配置域名 CNAME 解析，服务生效。

详情请参见 [域名接入](https://intl.cloud.tencent.com/document/product/570/10361)。

### 接入 ECDN 的域名是否必须完成域名备案？
系统是否检查域名备案与您选择的加速区域有关：
- 若加速区域包含中国境内区域，根据相关法规，您的接入域名必须完成工信部备案才可接入。
- 若加速区域仅为中国境外（包含港澳台）区域，您的接入域名无需接入工信部备案。

### ECDN 是否支持泛域名接入？

全站加速目前已经支持泛域名接入。

### ECDN 支持哪些回源方式？

<table style="display:table;" width="80%">
	<thead>
		<tr>
			<th colspan="1" style="text-align: center" width=15%> 回源方式 </th>
			<th colspan="1" style="text-align: center" width=70%> 回源方式说明 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center">择优回源 </td>
			<td>默认回源策略。</br>根据平台探测结果，回源时选择效果最佳的节点。 </td>
		</tr>
		<tr>
			<td style="text-align: center">分权重回源 </td>
			<td>根据源站权重系数，分比例回源。 </td>
		</tr>
		<tr>
			<td style="text-align: center">分主备回源 </td>
			<td>只要主源服务正常,回源时直接选择主源，仅当主源服务异常时，启用备源回源。 </td>
		</tr>
	</tbody>
</table>



<span id="port"></span>

### 加速端口（或访问端口）与回源端口有什么区别？

当使用 CDN 或 ECDN 加速时，两者的主要区别如下：

<table>
   <tr>
      <th style="width: 80px; text-align: center;">端口类型</th>
      <th style="width: 300px; text-align: center;">加速端口</th>
      <th style="width: 300px; text-align: center;">回源端口</th>
   </tr>
   <tr>
      <td style="width: 80px; text-align: center;">端口区别</td>
      <td style="width: 300px; text-align: left;">指 CDN/ECDN 的服务端口，也是客户端或用户访问边缘节点时的请求端口</td>
      <td style="width: 300px; text-align: left;">指源站的服务端口，也是 CDN/ECDN 节点访问源站时的请求端口</td>
   </tr>
   <tr>
      <td style="width: 80px; text-align: center;">端口取值</td>
      <td>仅支持80，443，8080端口</td>
      <td>1-65535</td>
   </tr>
</table>


>! 
> - 使用全站加速后，若客户端的请求端口与节点开放的服务端口不匹配，节点将无法加速客户端访问请求。  
> - 您可以通过 ECDN 域名管理页面指定节点回源端口。

### 控制台接入域名失败时如何处理?

域名接入时，常见的错误类型和处理措施如下：

<table style="display:table;" width="100%">
	<thead>
		<tr>
			<th colspan="1" style="text-align: center" width=30%> 错误类型 </th>
			<th colspan="1" style="text-align: center" width=70%> 错误说明及处理措施 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>CDN 配置对应域名已存在 </td>
			<td>您需要确认域名已从境内 CDN 和境外 CDN 下线删除后，才可以在全站加速平台添加域名。 </td>
		</tr>
		<tr>
			<td>加速域名未备案 </td>
			<td>当您加速区域包含中国境内时，根据相关法规，加速域名必须接入工信部域名备案系统。</br>若您只需要中国境外用户的访问体验，您可以在添加域名时取消勾选中国境内加速区域，则无需进行域名备案审查。 </td>
		</tr>
		<tr>
			<td>加速域名已存在 </td>
			<td>若域名已在当前账号下添加过，无需重复添加，可以直接使用。</br>若您的域名被其他账号接入，您可以通过 <a href='https://console.cloud.tencent.com/workorder/category'>工单系统</a> 提交域名持有证明，申请找回域名配置权限。 </td>
		</tr>
		<tr>
			<td>受限制域名 </td>
			<td>系统限制用户添加的域名，这些域名包括但不限于：腾讯或腾讯云内部域名、锁定的域名、黑名单封禁的域名。您可以通过 <a href='https://console.cloud.tencent.com/workorder/category'>提交工单</a> 申请受限制域名的配置权限。 </td>
		</tr>
		<tr>
			<td>域名数量超过系统限制 </td>
			<td>平台默认每个账号最多可添加200个加速域名配置，您可以删除已下线域名的配置或申请更高额度的域名数量限制。 </td>
		</tr>
		<tr>
			<td>域名格式非法 </td>
			<td>系统仅支持加速 ASCII 域名，非 ASCII 域名或包含非法字符的域名无法添加。 </td>
		</tr>
	</tbody>
</table>





