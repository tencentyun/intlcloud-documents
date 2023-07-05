
1. 登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在左侧导航栏中，单击**域名管理**进入域名管理页面，单击**添加域名**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Ds3Z834_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153247.png)
2. 域名配置
根据您的网站信息，配置如下：
<br>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/Aw8L098_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153500.png" width="80%">
<br>
如上图所示，当接入域名为泛域名，或已被其他用户接入，或首次接入一个新域名时，需要验证域名的归属权。若您的域名解析商为腾讯云，可以按照如下图配置 TXT 解析记录（针对主域名添加即可），完成验证即可添加该域名。更多详情请参见 <a href="https://intl.cloud.tencent.com/document/product/228/42693">域名归属权验证</a>。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/iX89276_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423154418.png">
3. 源站配置
源站的用途：源站即为存储网站资源的服务器，当用户请求的资源在 CDN 节点无缓存，节点会读取域名配置的源站信息，回源拉取资源并缓存在节点。因此，源站信息务必填写准确，保证 CDN 能正常回源取到对应的资源。
根据您的源站信息，配置如下。
<br>
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/8dKk701_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230423153800.png" width="90%">
<table>
<thead>
<tr>
<th>配置项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>源站类型</td>
<td>网站源站为稳定运行业务的自有服务器，<strong>选择“自有源”即可</strong></td>
</tr>
<tr>
<td>回源协议</td>
<td>只支持HTTP回源，<strong>回源协议选择“HTTP”即可。</strong><br>可以根据源站实际支持的协议类型，按需选择，确保选择的回源协议是源站支持的。</td>
</tr>
<tr>
<td>源站地址</td>
<td><strong>填写源站的服务器 IP 即可。</strong><br>• 支持配置多个 IP 作为源站，回源时会进行轮询回源；<br>• 支持增加配置端口（0 - 65535）和权重（1 - 100）：源站:端口:权重（端口可缺省：源站::权重），HTTPS 协议暂时仅支持443端口；<br>• 支持配置域名作为源站，此域名需要与业务加速域名不一致。</td>
</tr>
<tr>
<td>回源 HOST</td>
<td>• 定义：CDN 节点在回源时，在源站访问的站点域名，默认为加速域名。<br>•  源站地址与回源 HOST 的区别：源站配置的 IP/域名能够指引 CDN 节点回源时找到对应的源站服务器，服务器上可能存在若干 Web 站点，回源 HOST 指明了资源所在的站点。根据实际业务场景配置即可<br>• 如何填写：若通过加速域名即可回源获取到资源，无需修改回源 HOST；若需要通过非加速域名才能回源获取到资源，填写对应的域名即可。</td>
</tr>
</tbody></table>
4. 单击**确认添加**后，即可完成添加域名，同时，腾讯云 CDN 根据您的加速类型为您提供了该域名的推荐配置，您可以参考 [推荐配置](https://intl.cloud.tencent.com/document/product/228/32978) 来进行配置，或单击**返回域名管理**完成域名添加。
