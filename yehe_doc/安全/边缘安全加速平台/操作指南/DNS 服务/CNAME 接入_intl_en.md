With the [CNAME connection](https://intl.cloud.tencent.com/document/product/1145/45967#CNAME) method, you can connect your site to EdgeOne security/acceleration services simply by adding a record (subdomain), selecting the corresponding proxy mode, and adding the specified CNAME record at your DNS service provider. You don't need to transfer the DNS resolution permission to EdgeOne.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.


## Adding Record (Connection via Subdomain)[](id:add)
In CNAME connection, you can add a record to connect site subdomains to the corresponding service.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **DNS service** on the left sidebar.
2. On the DNS service page, select the target site and click **Add record**.
![](https://qcloudimg.tencent-cloud.cn/raw/4867bc46bd8a05f228f2630b7b41a285.png)
3. Enter the relevant parameters and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/8d0753634031df6bb467227f4567c40a.png)

**Parameter description:**

 - Record type: Origin server type.
 - Record value: Origin server address.

<table>
<thead>
<tr>
<th>Record Type</th>
<th>Sample Record Value</th>
<th>Usage Description</th>
</tr>
</thead>
<tbody><tr>
<td>A</td>
<td>8.8.8.8</td>
<td>Traffic to the corresponding host record (subdomain) will be forwarded to an IPv4 origin server at `8.8.8.8`.</td>
</tr>
<tr>
<td>AAAA</td>
<td>2400:cb00:2049:1::a29f:f9</td>
<td>Traffic to the corresponding host record (subdomain) will be forwarded to an IPv6 origin server at `2400:cb00:2049:1::a29f:f9`. EdgeOne supports dual-stack origin-pull by default.</td>
</tr>
<tr>
<td>CNAME</td>
<td>www.origin.com</td>
<td>Traffic to the corresponding host record (subdomain) will be forwarded to a domain origin server at `www.origin.com`.</td>
</tr>
</tbody></table>

 - Host record: It is equivalent to the prefix of a subdomain. If the root domain of the current site is `edgeone.com`, then common host records are as listed below:
 <table>
<thead>
<tr>
<th>Host Record Value</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>@</td>
<td>It directly resolves the domain as the root domain `edgeone.com`.</td>
</tr>
<tr>
<td>www</td>
<td>It is a common host record and resolves the domain as `www.edgeone.com`.</td>
</tr>
<tr>
<td>mail</td>
<td>It resolves the domain as `mail.edgeone.com` and is usually used for email services.</td>
</tr>
<tr>
<td>*</td>
<td>It is a wildcard and matches all other domains like `*.edgeone.com`.</td>
</tr>
</tbody></table>

 - Proxy mode: The CNAME connection method supports the following three service (proxy) modes. For more information, see [Proxy Mode](https://intl.cloud.tencent.com/document/product/1145/45968).
    - Proxy disabled
    - Proxy acceleration
    - Secure acceleration
 - CNAME: The CNAME suffix specified by the system varies by the selected proxy mode. You need to add the specified CNAME record at your DNS service provider.
 - HTTPS certificate: In CNAME connection, the system doesn't provide an EdgeOne universal certificate. You need to associate each subdomain with a certificate manually before you can use the HTTPS service normally.

## Switching to NS Connection[](id:change)
On the CNAME connection page, click **Switch to NS connection** in the top-right corner of the list to switch to NS connection. Then, you need to modify the NS record as required. After the modification takes effect, you will be notified by email, SMS, and Message Center. After the switch:
- All CNAME records and proxy mode settings will be retained. The "Proxy disabled" proxy mode set for records will become "DNS only".
- The custom certificates of all subdomains will be retained.

![](https://qcloudimg.tencent-cloud.cn/raw/416a5ce42de88a8f5ae132102dc95bfd.png)
