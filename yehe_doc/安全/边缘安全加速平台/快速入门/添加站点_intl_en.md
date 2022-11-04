## Overview
You can connect your site (i.e., second-level domain) to EdgeOne in the following two [connection methods](https://intl.cloud.tencent.com/document/product/1145/45967).
- Connect via NS (recommended): Transfer DNS records to EdgeOne and enable the security protection and acceleration services immediatly.
- Connect via CNAME: Continue using your current DNS service provider and add the specified CNAME record at it to enable the EdgeOne security protection and acceleration services.

## Connecting via NS (Recommended)
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Service Overview** on the left sidebar.
2. On the service overview page, click **Add Site** in the top-right corner.
3. On the site addition page, enter a valid second-level domain and click **Next**.
>?If a site has been connected to Edegone by another account, you need to reclaim it through [site verification](https://intl.cloud.tencent.com/document/product/1145/45969).

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
4. On the DNS configuration page, the system will automatically scan and import the original DNS records of your site. You can also add, delete, and modify records and configure the [proxy mode](https://intl.cloud.tencent.com/document/product/1145/45968). Then, click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/aa62a8c7d2247738bd21d85cb370d019.png)
5. Log in at the domain registrar of your site and modify the NS server records to the value specified in EdgeOne as instructed on the NS server modification page. For detailed directions, see [Modifying NS](#NSXG).
6. After modification, click **Complete** to redirect to the site overview page.
>?The time when the NS records take effect is subject to your domain registrar. After they take effect, the system will inform you by email, SMS, and Message Center.


## Connecting via CNAME
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Service Overview** on the left sidebar.
2. On the service overview page, click **Add Site** in the top-right corner.
3. On the site addition page, enter a valid second-level domain and click **Next**.
>?If a site has been connected to Edegone by another account, you need to reclaim it through [site verification](https://intl.cloud.tencent.com/document/product/1145/45969).

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
5. On the DNS configuration page, you can add, delete, and modify records and configure the [proxy mode](https://intl.cloud.tencent.com/document/product/1145/45968). Then, click **Access via CNAME**.
![](https://qcloudimg.tencent-cloud.cn/raw/93f56859b479d239090ef7f0698057a9.png)
6. On the site verification page, add a TXT record at your DNS service provider to verify your ownership of the site and click **Complete Verification**.
![](https://qcloudimg.tencent-cloud.cn/raw/c6e5de739623bc1a8758318c9a29665d.png)


## Modifying NS[](id:NSXG)
1. Log in at the domain registrar of your site. If you cannot confirm the registrar, query it at [ICANN WHOIS](https://lookup.icann.org/).
2. After login, disable the Domain Name System Security Extensions (DNSSEC) configuration.
3. Delete the original NS configuration and modify it to the value specified in EdgeOne.
4. Wait for the NS records to take effect. After they take effect, the system will inform you by email, Message Center, and SMS.

Configuration guides for major domain registrars:
- [Amazon](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-name-servers-glue-records.html#domain-name-servers-glue-records-adding-changing)
- [GoDaddy](https://sg.godaddy.com/zh/help/change-nameservers-for-my-domains-664)
- [Google Domains](https://support.google.com/domains/answer/3290309?hl%3Den)
- [Name.com](https://www.name.com/support/articles/205934547-changing-nameservers-for-dns-management)
- [Yahoo!](http://support.hostgator.com/articles/how-to-change-name-servers-with-yahoo-com)
