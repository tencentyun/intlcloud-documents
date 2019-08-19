After your domain name is bound to CDN, the system automatically assigns you a CNAME domain name suffixed with `.cdn.dnsv1.com` which can be viewed on the [Domain Name Management](https://console.cloud.tencent.com/cdn/access) page in the CDN Console. It cannot be accessed directly. Instead, you need to complete the CNAME configuration with the domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![](https://main.qcloudimg.com/raw/7f9a483270c68360fb7808461aea9845.png)

## CNAME verification
The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also run ping on the command line to check whether the CNAME record is in effect. If a domain name suffixed with `.sp.spcdntip.com` can be pinged, the domain name CNAME record has taken effect.

