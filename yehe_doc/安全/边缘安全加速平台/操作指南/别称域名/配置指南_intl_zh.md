本文将向您介绍创建别称域名、别称域名配置 CNAME 指向目标域名、别称域名配置证书、编辑和删除别称域名等相关操作。

## 前提条件
您需要成功 [购买](https://console.cloud.tencent.com/edgeone) 边缘安全加速平台（EdgeOne）产品（企业版），并完成 [接入站点](https://intl.cloud.tencent.com/document/product/1145/45966) 以及目标域名的创建。

## 新建别称域名

### 步骤1：创建别称域名
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧导航栏中，单击**别称域名**。
2. 在别称域名列表页，单击**新建别称域名**，配置相关参数，单击**确定**。<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8wtm193_1-en.png" width=800px>
<table>
<thead>
<tr>
<th width="10%">参数名称</th>
<th width="90%">参数详情</th>
</tr>
</thead>
<tbody><tr>
<td>别称域名</td>
<td>域名长度不超过81个字符，不支持泛域名如 <code>*.test.com</code>，如您当前站点的加速区域为中国境内，别称域名需在工信部完成备案。</td>
</tr>
<tr>
<td>目标域名</td>
<td>支持选择当前站点下“已生效”和“部署中”的接入域名，详情请参见 <a href="https://intl.cloud.tencent.com/document/product/1145/46354">CNAME接入</a> 和 <a href="https://intl.cloud.tencent.com/document/product/1145/46353">NS接入</a>。</td>
</tr>
<tr>
<td>证书配置</td>
<td><ul><li>不配置：不配置 HTTPS 证书，选择此方式的别称域名将只具备 HTTP 的访问能力。</li><li>SSL 托管证书：选择已托管至 SSL 的证书，如您需购买和上传自有证书请<a href="https://intl.cloud.tencent.com/contact-us">联系我们</a>。</li><li> 申请免费证书：平台实现免费证书的申请和自动更新，如您需选择此项，请先完成域名添加并在域名解析商将别称域名的 CNAME 指向目标域后再操作。</li></ul></td>
</tr>
</tbody></table>


### 步骤2：添加别称域名指向目标域名的 CNAME 记录
1. 别称域名添加成功后，状态默认为**不生效**，如下所示：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/va6E018_2-pro-en.png" width=800px>
2. 前往别称域名解析商添加指向目标域名的 CNAME 记录即可触发别称域名生效。
3. EdgeOne 会自动完成检测并将别称域名的状态调整为**已生效**。

### 步骤3：申请免费证书（可选）
若已在域名解析商将别称域名的 CNAME 指向目标域名，您可以在 EdgeOne 申请免费证书。   
1. 在 [别称域名列表页](https://console.cloud.tencent.com/edgeone/alias-domain)，单击**编辑**，选择**申请免费证书**。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/C7tD159_4-en.png" width=800px>
2. 单击**确定**，即可为别称域名申请和部署免费证书。 

## 编辑别称域名
1. 在 [别称域名列表页](https://console.cloud.tencent.com/edgeone/alias-domain)，选择别称域名，单击**编辑**。
2. 可按需修改目标域名和证书配置的类型，单击**确定**。

## 删除别称域名
>!
>- 未停用的别称域名不支持直接删除。
>- 别称域名一旦删除其数据不可恢复，请谨慎操作。

1. 在 [别称域名列表页](https://console.cloud.tencent.com/edgeone/alias-domain)，选择别称域名，单击**停用** > **删除**。
2. 在确认删除窗口中，单击**确定**。<br><img src="https://staticintl.cloudcachetci.com/yehe/backend-news/wrVH295_5-en.png" width=600px>

## 查询别称域名
您可在 [别称域名列表页](https://console.cloud.tencent.com/edgeone/alias-domain) 的查询输入框中输入别称域名的关键词，按下回车键即可完成查询操作。  
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8yBE228_6-en.png" width=800px>
