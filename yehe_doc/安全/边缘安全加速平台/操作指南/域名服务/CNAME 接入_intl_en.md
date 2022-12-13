In CNAME access mode, you can connect your site to EdgeOne security/acceleration services simply by adding a record (subdomain name), enabling proxy, and adding the specified CNAME record at your DNS service provider. You don't need to transfer the DNS resolution permission to EdgeOne.


## Adding a record (connection via subdomain)[](id:add)
In CNAME access mode, you can add a record to connect site subdomain names to the corresponding service.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Domain Name Service** on the left sidebar.
2. On the page that appears, select the target site and click **Add domain name**.
![](https://qcloudimg.tencent-cloud.cn/raw/4867bc46bd8a05f228f2630b7b41a285.png)
3. Enter the relevant parameters and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/8d0753634031df6bb467227f4567c40a.png)
**Parameter description:**
  - Acceleration domain name: Enter the subdomain name to be accelerated. Only the prefix of the subdomain name is required.
  - Origin type: Select "IPv4", "IPv6", or "domain name" as needed.
  - Origin address: Enter the origin address according to the origin type. Examples are given in the following table.
<table>
<thead>
<tr>
<th>Origin Type</th>
<th>Example of Origin Address</th>
<th>Usage Description</th>
</tr>
</thead>
<tbody><tr>
<td>IPv4</td>
<td>8.8.8.8</td>
<td>Traffic is forwarded to an IPv4 origin server at `8.8.8.8`.</td>
</tr>
<tr>
<td>IPv6</td>
<td>2400:cb00:2049:1::a29f:f9</td>
<td>Traffic is forwarded to an IPv6 origin server at `2400:cb00:2049:1::a29f:f9`.<br>EdgeOne supports dual-stack origin-pull by default.</td>
</tr>
<tr>
<td>Domain Name</td>
<td>www.origin.com</td>
<td>Traffic is forwarded to a domain origin server at `www.origin.com`.</td>
</tr>
</tbody></table>

 - Proxy mode: Set the proxy mode to **Proxied** or **Only DNS**. For more information, see [Proxy Mode](https://intl.cloud.tencent.com/document/product/1145/45968).
 - CNAME: A CNAME record is generated when proxy is enabled. You need to add the CNAME record at your DNS service provider.
 - HTTPS certificate: When CNAME access is used, EdgeOne does not provide a universal certificate. In this case, you need to associate each subdomain name with a certificate manually before you can use the HTTPS service normally.
4. After saving the record, EdgeOne will assign a CNAME record to your subdomain name. You need to configure the CNAME record at your DNS service provider before you can direct user access to EdgeOne nodes and make the acceleration take effect.
5. After the configuration, if a green icon appears in the CNAME column, the CNAME record has taken effect, and the subdomain name is accelerated.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/3CAT513_3.png" style="zoom:150%;" />

