With the NS connection method, you can modify the NS to transfer your site's DNS resolution permission to EdgeOne. This quickly enables the EdgeOne security/acceleration services while implementing a stable and professional DNS service.

## NS Record[](id:record)
EdgeOne DNS supports the smart DNS service for various record types to intelligently return the optimal split zone based on end users' geographical locations and ISPs.
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Domain Name Service** on the left sidebar.
2. On the page that appears, select the target site and click **DNS records**.
3. On the page you enter, select the target record, click **Edit** to edit the parameters, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f87f22a64d1495d1ae5a44d2bd05dded.png)

**Parameter description:**
 - Record type and value: Different record types have different purposes.

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
<td>It points a domain name to a public network IPv4 address such as `8.8.8.8`.</td>
</tr>
<tr>
<td>AAAA</td>
<td>2400:cb00:2049:1::a29f:f9</td>
<td>It points a domain name to a public network IPv6 address.</td>
</tr>
<tr>
<td>CNAME</td>
<td>cname.edgeone.com</td>
<td>It points a domain name to another domain, from which the final IP address will be resolved.</td>
</tr>
<tr>
<td>MX</td>
<td>10 mail.edgeone.com</td>
<td>It is used for email servers. The record value and priority parameters are provided by email service providers. If there are multiple MX records, the lower the priority value, the higher the priority.</td>
</tr>
<tr>
<td>TXT</td>
<td>ba21a62exxxxxxxxxxcf5f06e</td>
<td>It identifies and describes a domain name and is usually used for domain verification and as SPF records (for anti-spam).</td>
</tr>
<tr>
<td>NS</td>
<td>ns01.edgeone.com</td>
<td>If you need to authorize a subdomain name to another DNS service provider for DNS resolution, you need to add an NS record. You cannot add an NS record for a root domain name.</td>
</tr>
<tr>
<td>SRV</td>
<td>1 5 7001 srvhostname.example.com</td>
<td>It identifies a service used by a server and is commonly used in Microsoft directory management.</td>
</tr>
<tr>
<td>CAA</td>
<td>0 issue trustasia.com</td>
<td>It specifies CAs to issue certificates for sites.</td>
</tr>
</tbody></table>

>? For an A, AAAA, or CNAME record, if [proxy acceleration or secure acceleration](https://intl.cloud.tencent.com/document/product/1145/45968) is enabled, the record value will be the origin server address for eventual origin-pull after proxy.

 - Host record: It is equivalent to the prefix of a subdomain. If the root domain of the current site is `edgeone.com`, then common host records are as listed below:

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
<th>SRV</th>
<th>CAA</th>
</tr>
</thead>
<tbody><tr>
<th>A</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
<tr>
<th>AAAA</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
<tr>
<th>CNAME</th>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<th>MX</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
<tr>
<th>NS</th>
<td>×</td>
<td>×</td>
<td>×</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>×</td>
<td>×</td>
</tr>
<tr>
<th>TXT</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
<tr>
<th>SRV</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
<tr>
<th>CAA</th>
<td>✓</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>×</td>
<td>✓</td>
<td>✓</td>
<td>✓</td>
</tr>
</tbody></table>

 - Proxy mode: Select **Only DNS** or **Enable proxy** based on the record type.

<table>
<thead>
<tr>
<th>Record Type</th>
<th>Proxy Mode</th>
</tr>
</thead>
<tbody><tr>
<td>A/AAAA/CNAME</td>
<td>Support both <strong>Only DNS</strong> and <strong>Enable proxy</strong>.</td>
</tr>
<tr>
<td>MX/TXT/NS/SRV/CAA</td>
<td>Only support <strong>Only DNS</strong>.</td>
</tr>
</tbody></table>

>?
>- In the case that there are multiple DNS records contain the same host record (the same subdomain prefix), if the proxy is enabled for only one record, the other records will be invalid.
>- When multiple DNS records contain the same host record (i.e., the same subdomain prefix): Proxy can be enabled for multiple A/AAAA records at the same time, but for only one CNAME record.
 - TTL: It is the DNS record cache time. Generally, the shorter the TTL, the shorter the cache time, and the faster the record value will take effect when it is updated, but the DNS speed will be slightly affected.
    - Available TTL values include: Automatic, 1 minute, 2 minutes, 5 minutes, 10 minutes, 15 minutes, 30 minutes, 1 hour, 2 hours, 5 hours, 12 hours, and 1 day. If you select **Automatic**, the system will configure TTL to 300 seconds.
    - How to configure TTL:
      - If the record value changes infrequently, select one hour or longer to speed up DNS resolution.
      - If the record value changes frequently, select a shorter TTL value such as one minute, which, however, may slightly slow down DNS resolution.
>?
>- In proxy acceleration, the TTL is **Automatic** by default and cannot be modified.
>- In actual conditions, TTL is not necessarily applied to LDNS cache configuration, which usually makes the time it takes for the record update to take effect much longer than the TTL.

## DNS Configuration
Advanced configuration items such as DNSSEC, custom NS, and CNAME acceleration are supported.

### DNSSEC[](id:dnsses)
DNS Security Extension (DNSSEC) uses a digital signature to authenticate the DNS data source in order to effectively protect the security and integrity of DNS resolution results. It is commonly used to prevent DNS spoofing and DNS cache poisoning.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Domain Name Service** on the left sidebar.
2. On the page that appears, select the target site and click **DNS configuration**.
3. On the DNS configuration page, click ![](https://qcloudimg.tencent-cloud.cn/raw/bfcf61e83f25591bfdd612e3faf66596.png) in the DNSSEC module and confirm the operation. Then the DS information will be generated.
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

1. On the [Domain Name Service](https://console.cloud.tencent.com/edgeone/dns?tab=config) page, select the target site and click **DNS configuration**.
2. On the DNS configuration page, click ![](https://qcloudimg.tencent-cloud.cn/raw/20efaa7f4ecc99b93da623f1c61784ac.png) in the custom NS module, enter a custom NS domain name, and click **Add**.
3. After adding a custom NS successfully, **you need to add its glue records at your domain registrar for it to take effect**.

### CNAME acceleration[](id:up)
Once enabled, CNAME acceleration can effectively accelerate DNS resolution. If multi-level CNAME records are set in EdgeOne DNS for a domain, the system will directly provide the final IP DNS resolution result to reduce the number of resolutions. This feature is enabled by default.
1. On the [Domain Name Service](https://console.cloud.tencent.com/edgeone/dns?tab=config) page, select the target site and click **DNS configuration**.
2. On the DNS configuration page, you can toggle CNAME acceleration on or off.
>? To directly get the final IP DNS resolution result, all multi-level CNAME records must be in EdgeOne DNS.


