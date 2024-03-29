### 私有域解析 Private DNS 限制
当前使用私有域解析 Private DNS 存在如下限制：
>!
>- 腾讯云默认 DNS 为：`183.60.83.19`，`183.60.82.98`，若不使用腾讯云默认 DNS，将无法使用私有域解析 Private DNS 提供的服务。如需修改，请您参考 [获取内网 IP 地址和设置 DNS](https://intl.cloud.tencent.com/document/product/213/17941)。
>- 如您有更进一步的业务场景需求，可通过商务渠道或 [在线咨询](https://intl.cloud.tencent.com/contact-sales) 进行反馈。

<table>
<thead>
  <tr>
    <th width="15%">限制项</th>
    <th>限制阈值</th>
    <th width="35%">说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>解析记录数量</td>
    <td>10万条</td>
    <td>同一个 UIN 账号下最多支持添加10万条 DNS 解析记录。</td>
  </tr>
  <tr>
    <td>域名数</td>
    <td>500个</td>
    <td>同一个 UIN 账号下最多仅支持创建私有域名数量为500个。</td>
  </tr>
  <tr>
    <td>TTL</td>
    <td>1 - 86400s</td>
    <td>解析记录在 DNS 服务器中的存留时间，支持自定义输入。<br>
DNS 查询存在 TTL 缓存机制，私有域解析 Private DNS 请求量统计取实际回源请求数量并计费（需设置本地 NSCD 缓存，以减少请求回源次数）。
		</td>
  </tr>
  <tr>
    <td>开放地域</td>
    <td>北京、上海、广州、成都、重庆、武汉、济南、石家庄、南京、合肥、沈阳、长沙、郑州、西安、福州、杭州、中国香港、硅谷、新加坡、法兰克福、雅加达，曼谷、孟买、弗吉尼亚、莫斯科、东京、首尔、多伦多</td>
    <td>开放地域即为私有域可关联 VPC 地域。</td>
  </tr>
  <tr>
    <td>创建私有域</td>
		<td>系统默认仅支持创建 符合 <a href="https://www.iana.org/domains/root/db">IANA</a> 规范的 TLD。如需自定义可购买 <a href="https://buy.intl.cloud.tencent.com/privatedns">增值服务 - 非标 TLD</a> 后创建</td>
    <td>参考资料：<a href="https://www.iana.org/domains/root/db">根域名数据库</a>。</td>
  </tr>
  <tr>
    <td>DNS 每秒请求</td>
    <td>根据 VPC 粒度限制每秒请求2000QPS</td>
    <td>VPC 内每秒请求 DNS 峰值超过限制阈值后，将面临限速风险，可用性 SLA（99.99%）将无法保证。</td>
  </tr>
	  <tr>
    <td>子域名递归解析</td>
    <td>-</td>
    <td>私有域解析 Private DNS 开启子域名递归解析后，未配置记录将转至公共 DNS 查询。如未开启该功能，将无法正常解析未配置的子域名，请谨慎操作。</td>
  </tr>
	<tr>
    <td>CNAME 加速</td>
    <td>-</td>
    <td>如您已设置 CNAME 记录，开启 CNAME 加速后，将同步返回 CNAME 记录目标 IP（使用该功能建议开启“子域名递归解析”，否则当 CNAME 记录目标 IP 需出公网查询时无法返回最终结果）。</td>
  </tr>
</tbody>
</table>

### 负载均衡限制
>?
>- “负载均衡” 条数：相同主机、相同记录类型允许添加的条数。
>- 超出额度后不能进行正常添加。若您需添加负载均衡条数，您可购买 [增值服务优惠包](https://www.tencentcloud.com/document/product/1097/50828) 进行使用。
>

<table>
<thead>
  <tr>
    <th width="17%">记录类型</th>
    <th>“负载均衡” 条数</th>
		<th>备注</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>A</td>
    <td>10</td>
		<td>-</td>
  </tr>
  <tr>
    <td>AAAA</td>
    <td>10</td>
		<td>-</td>
  </tr>
  <tr>
    <td>TXT</td>
    <td>20</td>
		<td>TXT 负载均衡不支持权重设置。</td>
  </tr>
	  <tr>
    <td>CNAME</td>
    <td>5</td>
		<td>-</td>
  </tr>
		  <tr>
    <td>MX</td>
    <td>50</td>
		<td>-</td>
  </tr>
		  <tr>
    <td>PTR</td>
    <td>PTR 记录不支持负载均衡。</td>
		<td>-</td>
  </tr>
</tbody>
</table>
