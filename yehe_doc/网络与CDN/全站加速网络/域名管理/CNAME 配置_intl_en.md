After your domain name is bound to ECDN, the system automatically assigns you a CNAME domain name suffixed with `.dsa.dnsv1.com` which can be viewed on the [Domain Name Management](https://console.cloud.tencent.com/ecdn/access) page in the CDN Console. It cannot be accessed directly. Instead, you need to complete the CNAME configuration with the domain name service provider first. When the configuration takes effect, you can use the CDN acceleration service.
![](https://main.qcloudimg.com/raw/d2772d1596ead081355ae17d2eb7062b.png)

## CNAME verification
The time it takes for a CNAME record to take effect varies by DNS service provider. It is generally within half an hour. You can also run ping on the command line to check whether the CNAME record is in effect. If a domain name suffixed with`.dsa.sp.spcdntip.com` or `.dsa.p23.tc.cdntip.com` can be pinged, the domain name CNAME record has taken effect.

