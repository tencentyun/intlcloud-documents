With the [NS connection](https://intl.cloud.tencent.com/document/product/1145/45967#NS) method, you can modify the NS record to transfer your site's DNS resolution permission to EdgeOne. This quickly enables the EdgeOne security/acceleration services while implementing a stable and professional DNS service.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Record Management[](id:record)
EdgeOne DNS supports the smart DNS service for various record types to intelligently return the optimal split zone based on end users' geographical locations and ISPs.
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **DNS service** on the left sidebar.
2. On the DNS service page, select the target site and click **Record management**.
3. On the record management page, select the target record, click **Edit** to edit the parameters, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f87f22a64d1495d1ae5a44d2bd05dded.png)

**Parameter description:**
 - Record type and value: Different record types have different purposes.
<table>
<thead>
<tr>
<th align="left">Record Type</th>
<th align="left">Sample Record Value</th>
<th align="left">Usage Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">A</td>
<td align="left">8.8.8.8</td>
<td align="left">It points a domain to a public network IPv4 address such as `8.8.8.8`.</td>
</tr>
<tr>
<td align="left">AAAA</td>
<td align="left">2400:cb00:2049:1::a29f:f9</td>
<td align="left">It points a domain to a public network IPv6 address.</td>
</tr>
<tr>
<td align="left">CNAME</td>
<td align="left">cname.edgeone.com</td>
<td align="left">It points a domain to another domain, from which the final IP address will be resolved.</td>
</tr>
<tr>
<td align="left">MX</td>
<td align="left">Priority: 10. Record value: mail.edgeone.com</td>
<td align="left">It is used for email servers. The record value and priority parameters are provided by email service providers. If there are multiple MX records, the lower the priority value, the higher the priority.</td>
</tr>
<tr>
<td align="left">TXT</td>
<td align="left">ba21a62exxxxxxxxxxcf5f06e</td>
<td align="left">It identifies and describes a domain and is usually used for domain verification and as SPF records (for anti-spam).</td>
</tr>
<tr>
<td align="left">NS</td>
<td align="left">ns01.edgeone.com</td>
<td align="left">If you need to authorize a subdomain to another DNS service provider for DNS resolution, you need to add an NS record. You cannot add an NS record for a root domain.</td>
</tr>
</tbody></table>

>? For an A, AAAA, or CNAME record, if [proxy acceleration or secure acceleration](https://intl.cloud.tencent.com/document/product/1145/45968) is enabled, the record value will be the origin server address for eventual origin-pull after proxy.
 - Host record: It is equivalent to the prefix of a subdomain. If the root domain of the current site is `edgeone.com`, then common host records are as listed below:
<table>
<thead>
<tr>
<th align="left">Host Record Value</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">@</td>
<td align="left">It directly resolves the domain as the root domain <code>edgeone.com</code>.</td>
</tr>
<tr>
<td align="left">www</td>
<td align="left">It is a common host record and resolves the domain as <code>www.edgeone.com</code>.</td>
</tr>
<tr>
<td align="left">mail</td>
<td align="left">It resolves the domain as <code>mail.edgeone.com</code> and is usually used for email services.</td>
</tr>
<tr>
<td align="left">*</td>
<td align="left">It is a wildcard and matches all other domains like <code>*.edgeone.com</code>.</td>
</tr>
</tbody></table>
 For the same host record, you can create multiple record types, which can or cannot coexist as follows:
<table>
<thead>
<tr>
<th>Record Type</th>
<th>A</th>
<th>AAAA</th>
<th>CNAME</th>
<th>MX</th>
<th>NS</th>
<th>TXT</th>
</tr>
</thead>
<tbody><tr>
<th>A</th>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
</tr>
<tr>
<th>AAAA</th>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
</tr>
<tr>
<th>CNAME</th>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<th>MX</th>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
</tr>
<tr>
<th>NS</th>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>&#10003;</td>
<td>×</td>
</tr>
<tr>
<th>TXT</th>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
<td>×</td>
<td>&#10003;</td>
</tr>
</tbody></table>
 - Proxy mode: You can select one of the following three modes: **DNS only, proxy acceleration, and secure acceleration**. The proxy modes that can be enabled vary by record type.
<table>
<thead>
<tr>
<th align="left">Record Type</th>
<th align="left">Proxy Mode</th>
</tr>
</thead>
<tbody><tr>
<td align="left">A/AAAA/CNAME</td>
<td align="left">You can select <strong>DNS only, proxy acceleration, or secure acceleration</strong>. The default mode is secure acceleration.</td>
</tr>
<tr>
<td align="left">MX/TXT/NS</td>
<td align="left">You can only select <strong>DNS only</strong>.</td>
</tr>
</tbody></table>

>?
>- For the same host record (subdomain), once proxy acceleration or secure acceleration is enabled, other record types for which the proxy is not enabled will become invalid.
>- For the same host record (subdomain), you can enable proxy acceleration or secure acceleration for multiple A/AAAA records. However, for the CNAME record type, no matter whichever the proxy mode is, only one record can exist.
 - TTL: It is the DNS record cache time. Generally, the shorter the TTL, the shorter the cache time, and the faster the record value will take effect when it is updated, but the DNS speed will be slightly affected.
    - Currently, the following TTL values are available: Automatic, 1 minute, 2 minutes, 5 minutes, 10 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, 5 hours, 12 hours, and 1 day. If you select **Automatic**, the system will configure TTL to 300 seconds.
    - How to configure TTL:
      - If the record value changes infrequently, select one hour or longer to speed up DNS resolution.
      - If the record value changes frequently, select a shorter TTL value such as one minute, which, however, may slightly slow down DNS resolution.
>?
> - In proxy acceleration/secure acceleration, the TTL is **Automatic** by default and cannot be modified.
>- In actual conditions, TTL is not necessarily applied to LDNS cache configuration, which usually makes the time it takes for the record update to take effect much longer than the TTL.


## Switching to CNAME Connection[](id:change)
On the NS connection page, you can click **Switch to CNAME connection** in the top-right corner of the list to switch to CNAME connection. Upon the first switch, you need to [verify the site](https://intl.cloud.tencent.com/document/product/1145/45969). If the site has been verified, verification will be skipped to directly complete the switch. After the switch:
- Original DNS records will be retained. A, AAAA, and CNAME records can be edited/deleted, while MX, NS, and TXT records can be deleted only.
- The proxy modes of all records will be inherited. After the switch, the "DNS only" proxy mode set for records will become "Proxy disabled".
- The EdgeOne universal certificate will be retained. However, it cannot be automatically updated in CNAME connection mode and will be automatically deleted upon expiration.
- The custom certificates of all subdomains will be retained.

![](https://qcloudimg.tencent-cloud.cn/raw/5380efeffaf42d7928e3456046e267ad.png)


## Advanced Configurations
Advanced configuration items such as DNSSEC, custom NS, and CNAME acceleration are supported.

### DNSSEC[](id:dnsses)
DNS Security Extension (DNSSEC) uses a digital signature to authenticate the DNS data source in order to effectively protect the security and integrity of DNS resolution results. It is commonly used to prevent DNS spoofing and DNS cache poisoning.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **DNS service** on the left sidebar.
2. On the DNS service page, select the target site and click **Advanced configuration**.
3. On the advanced configuration page, click ![](https://qcloudimg.tencent-cloud.cn/raw/20efaa7f4ecc99b93da623f1c61784ac.png) in the DNSSEC module and confirm the operation. Then, the DS information will be generated.
![](https://qcloudimg.tencent-cloud.cn/raw/214fa31e1c3006e90fd713639871c33b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/9ad64e8e0a0b9e1054ee623a0c83e77a.png)
4. Add a DS record at your domain registrar according to the above information. For detailed directions with certain registrars, see the following documents:
 - [DNSimple](https://support.dnsimple.com/articles/cloudflare-ds-record/)
 - [GoDaddy](https://ph.godaddy.com/help/add-a-ds-record-23865)
 - [Google Domains](https://support.google.com/domains/answer/6387342?hl=en)
 - [name.com](https://www.name.com/support/articles/205439058-Managing-DNSSEC)
 - [Public Domain Registry](http://manage.publicdomainregistry.com/kb/answer/1909)

### Custom NS[](id:customize)
The custom NS feature allows you to create a name server (NS) dedicated to your own site to replace the default assigned name server. After creation, EdgeOne will automatically assign an IP to it.
>?Custom NS has the following limits:
>- Only a subdomain (ns.example.com) of the current site (example.com) can be used as a custom NS.
>- You can add only two to five custom name servers.
>- If you enable custom NS for the first time, you need to add two custom name servers, and the custom names must be different from existing DNS records.

1. On the [DNS service page](https://console.cloud.tencent.com/edgeone/dns?tab=config), select the target site and click **Advanced configuration**.
2. On the advanced configuration page, click ![](https://qcloudimg.tencent-cloud.cn/raw/20efaa7f4ecc99b93da623f1c61784ac.png) in the custom NS module, enter a custom NS domain, and click **Add**.
3. After adding a custom NS successfully, **you need to add its glue record at your domain registrar for it to take effect**.

### CNAME acceleration[](id:up)
Once enabled, CNAME acceleration can effectively accelerate DNS resolution. If multi-level CNAME records are set in EdgeOne DNS for a domain, the system will directly provide the final IP DNS resolution result to reduce the number of resolutions. This feature is enabled by default.

1. On the [DNS service page](https://console.cloud.tencent.com/edgeone/dns?tab=config), select the target site and click **Advanced configuration**.
2. On the advanced configuration page, you can toggle CNAME acceleration on or off.
>? To directly get the final IP DNS resolution result, all multi-level CNAME records must be in EdgeOne DNS.


