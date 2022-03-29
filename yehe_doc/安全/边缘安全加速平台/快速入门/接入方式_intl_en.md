EdgeOne provides two connection methods for the integrated layer-7 edge service:

- NS connection (recommended): You can transfer DNS records to EdgeOne and quickly enable the security protection and acceleration services.
- CNAME connection: You can continue using your current DNS service provider and add the specified CNAME record at it to enable the EdgeOne security protection and acceleration services.



The proxy modes supported by the two connection methods and how they take effect are different as detailed below:

| Connection Method   | Proxy Mode                   | Remarks                                          |
| ---------- | -------------------------- | --------------------------------------------- |
| NS connection    | DNS only, proxy acceleration, and secure acceleration | You need to modify the NS server. After you select a proxy mode, the proxy will automatically take effect.  |
| CNAME connection | Proxy acceleration and secure acceleration         | You need to verify your site ownership. The proxy will take effect after you add a CNAME record as needed. |

>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## NS Connection (Recommended)[](id:NS)
During NS connection, you need to first modify the NS server records as required. After successful modification, the site's DNS service will be provided by EdgeOne. On the [DNS service page](https://console.cloud.tencent.com/edgeone/dns), you can manage records, add host records (subdomains), and select different proxy modes. After you select a proxy mode, the system will automatically distribute basic **site acceleration/anti-DDoS** configurations by site. You can also log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) to configure certificate management, site acceleration, and WAF.
![](https://qcloudimg.tencent-cloud.cn/raw/c40a7387cb823e5194972695e8839d7d.png)

>?During NS connection, the system will apply for a free universal EdgeOne certificate for the root domain (example.com) and third-level wildcard domain (*.example.com).



## CNAME Connection[](id:CNAME)
During CNAME connection, you need to add the host record (subdomain), corresponding record type (origin server type), and record value (origin server address), and select a proxy mode on the CNAME connection page. The system will generate the specific CNAME record. Then, you need to add the CNAME record at your DNS service provider for the proxy service to take effect.
![](https://qcloudimg.tencent-cloud.cn/raw/aa62a8c7d2247738bd21d85cb370d019.png)