### Private DNS Limits
Currently, Private DNS has the following limits:
>!
>- Tencent Cloud's default DNS IP addresses are `183.60.83.19` and `183.60.82.98`. If you don't use the default DNS IP addresses, you will not be able to use the Private DNS service. If you need to modify them, please see [Getting Private IP Addresses and Setting DNS](https://intl.cloud.tencent.com/document/product/213/17941).
>- If you have further requirements for your business scenarios, you can contact your sales rep or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

<table>
<thead>
  <tr>
    <th width="17%">Item</th>
    <th>Threshold</th>
		<th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Number of DNS records</td>
    <td>100,000</td>
    <td>Up to 100,000 DNS records can be added under each UIN account.</td>
  </tr>
  <tr>
    <td>Number of domain names</td>
    <td>500</td>
    <td>Up to 500 private domain names can be created under each UIN account.</td>
  </tr>
  <tr>
    <td>TTL</td>
    <td>1–86400s</td>
    <td>This is the retention time of a DNS record on the DNS server and can be customized.</td>
  </tr>
	  <tr>
    <td>Available regions</td>
    <td>Jakarta, Tokyo, Hong Kong(China), Frankfurt, Moscow, South Korea, East America, North America, Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, and Nanjing</td>
		<td>An available region is a VPC region that can be associated with a private domain.</td>
  </tr>
		  <tr>
    <td>Private domain creation</td>
    <td>You can only create domain names (except .com.cn) that comply with the IANA specifications.</td>
		<td>For more information, please see <a href="https://www.iana.org/domains/root/db">Root Zone Database</a>.</td>
  </tr>
</tbody>
</table>

### Round-Robin DNS Record Limits
>?"Number of Round-Robin DNS Records" refers to the number of records of the same record type that can be added for the same host.

<table>
<thead>
  <tr>
    <th width="17%">Record Type</th>
    <th>Number of Round-Robin DNS Records</th>
		<th>Remarks</th>
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
		<td>TXT round-robin DNS records don't support weight configuration.</td>
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
