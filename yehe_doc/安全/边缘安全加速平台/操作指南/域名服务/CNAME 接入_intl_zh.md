在 CNAME 接入方式下，用户无需将 DNS 解析权转移给 EdgeOne，只需添加记录（子域名）并开启代理，在 DNS 解析商处添加指定的 CNAME 记录，即可接入 EdgeOne 安全/加速服务。


## 添加记录（子域名接入）[](id:add)
在 CNAME 接入方式下，通过添加记录来为该站点的子域名接入相应的服务。

1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**域名服务**。
2. 在域名服务页面，选择所需站点，单击**添加域名**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/vePh814_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_c1a06409-5016-47ba-8bcd-3959a02e0240.png)
3. 填写相关参数，单击**保存**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Knm7963_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_5b09d140-e69c-4edc-b934-c7398fe3ad64.png)
**参数说明：**
  - 加速域名：填写需开启加速的子域名，仅需输入子域名的前缀。
  - 源站类型：可选择 IPv4/IPv6/域名。
  - 源站地址：源站类型和源站地址示例如下
<table>
<thead>
<tr>
<th>源站类型</th>
<th>源站地址示例</th>
<th>用途说明</th>
</tr>
</thead>
<tbody><tr>
<td>IPv4</td>
<td>8.8.8.8</td>
<td>回源到一个 IPv4 源站，源站地址为 8.8.8.8</td>
</tr>
<tr>
<td>IPv6</td>
<td>2400:cb00:2049:1::a29f:f9</td>
<td>回源到一个 IPv6 源站，源站地址为 2400:cb00:2049:1::a29f:f9。<br>EdgeOne 默认支持双栈回源</td>
</tr>
<tr>
<td>域名</td>
<td>www.origin.com</td>
<td>回源到一个域名源站，源站地址为 www.origin.com</td>
</tr>
</tbody></table>

 - 代理模式：支持开启/关闭代理，更多详情请参见 [代理模式](https://intl.cloud.tencent.com/document/product/1145/45968)。
 - CNAME：开启代理后系统自动生成，用户需在 DNS 服务商处添加该 CNAME 记录。
 - HTTPS 证书：在 CNAME 接入方式下，系统不提供 EdgeOne 通用证书。需要手动为每个子域名关联证书，方可正常使用 HTTPS 服务。
4. 保存记录之后，EdgeOne 会给您的子域名分配一个 CNAME，您还需要前往您的 DNS 解析服务商完成 CNAME 配置，才可以将用户的访问指向 EdgeOne 节点，使加速生效。
5. 配置完成之后，域名服务列表中，CNAME 列出现绿色的 icon 则表示该 CNAME 记录已生效，该子域名正常加速中。
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3uIu516_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_ada06b1c-7d8c-494a-950e-c8e20435fff0.png" style="zoom:150%;" />

