### Private DNS Limits
Currently, Private DNS has the following limits:
>!
>- Tencent Cloud's default DNS servers are `183.60.83.19` and `183.60.82.98`. If you don't use the default DNS servers, you will be unable to use the Private DNS service. If you need to modify it, see [Getting Private IP Addresses and Setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
>- For more scenario requirements, you can give feedback via your rep or [submit a ticket](https://intl.cloud.tencent.com/contact-sales).

<table>
<thead>
  <tr>
    <th width="15%">Limit Item</th>
    <th>Threshold</th>
    <th width="35%">Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Number of DNS records</td>
    <td>100,000</td>
    <td>Up to 100,000 DNS records can be added under each UIN account.</td>
  </tr>
  <tr>
    <td>Number of domains</td>
    <td >500</td>
    <td>Up to 500 private domains can be created under each UIN account.</td>
  </tr>
  <tr>
    <td>TTL</td>
    <td>1 - 86,400s</td>
    <td>This is the retention time of a DNS record on the DNS server and can be customized.<br>
There is a cache TTL mechanism for DNS queries. The DNS queries in Private DNS are counted based on the actual origin-pull requests and billed. You need to set the local NSCD cache to reduce original pulls.
		</td>
  </tr>
  <tr>
    <td>Available regions</td>
    <td>Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, Wuhan, Jinan, Shijiazhuang, Nanjing, Hefei, Shenyang, Changsha, Zhengzhou, Xi'an, Fuzhou, Hangzhou, Hong Kong, Silicon Valley, Singapore, Frankfurt, Jakarta, Bangkok, Mumbai, Virginia, Moscow, Tokyo, Seoul, Toronto</td>
    <td>An available region is a VPC region that can be associated with a private domain.</td>
  </tr>
  <tr>
    <td>Private domain creation</td>
		<td>By default, the system only supports creation of TLDs complying with <a href="https://www.iana.org/domains/root/db">IANA</a> standards. To create custom domains, purchase the <a href="https://buy.intl.cloud.tencent.com/privatedns">Value–Added Service - Non-Standard TLDs</a> first.</td>
    <td>For more information, see <a href="https://www.iana.org/domains/root/db">Root Zone Database</a>.</td>
  </tr>
  <tr>
    <td>DNS queries per second </td>
    <td>This item is limited to 2,000 QPS based on the VPC rules.</td>
    <td>If the DNS query peak per second exceeds the threshold, there will be a risk of access limit, and the availability stated in SLA (99.99%) cannot be guaranteed.</td>
  </tr>
	  <tr>
    <td>Recursive Subdomain Resolution</td>
    <td>-</td>
    <td>After the Recursive Subdomain Resolution feature of Private DNS is enabled, queries for a subdomain for which no records are set will be forwarded to the Public DNS. If this feature is not enabled, such queries cannot be properly resolved. </td>
  </tr>
	<tr>
    <td>CNAME flattening</td>
    <td>-</td>
    <td>If you have set a CNAME record, the target IP of the CNAME will be synchronously returned after the CNAME flattening feature is enabled. We recommend enabling the Recursive Subdomain Resolution feature before using this feature. Otherwise, no final result can be returned if the target IP of the CNAME record requires query in the Public DNS.</td>
  </tr>
</tbody>
</table>

### Round-Robin DNS Record Limits
>?
>- Number of Round-Robin DNS Records refers to the number of records of the same host and the same record type that can be added.
>- Those out of the limit cannot be properly added. To set the number of round-robin DNS records, purchase a [value-added service package](https://www.tencentcloud.com/document/product/1097/50828) first.
>

<table>
<thead>
  <tr>
    <th width="17%">Record Type</th>
    <th>Number of Round-Robin DNS Records</th>
		<th>Notes</th>
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
    <td>Select “TXT”.</td>
    <td>20</td>
		<td>TXT round-robin DNS doesn’t support weight configuration.</td>
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
    <td>PTR doesn't support round-robin DNS.</td>
		<td>-</td>
  </tr>
</tbody>
</table>
