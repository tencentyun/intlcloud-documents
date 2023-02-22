 ## Overview
You can purchase and connect to EdgeOne by site (i.e., second-level domain). The following two [connection methods](https://intl.cloud.tencent.com/document/product/1145/45967) are supported:
- NS access (recommended): You can transfer DNS records to EdgeOne and quickly enable the security protection or acceleration services.
- CNAME access: You can continue using your current DNS service provider and add the specified CNAME record at it to enable the EdgeOne security protection or acceleration services.

## NS Access (Recommended)
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Add site**.
![](https://qcloudimg.tencent-cloud.cn/raw/feaf8979272485d38100b9cd7f127339.png)
2. On the site addition page, enter a valid second-level domain and click **Next**.
>?You cannot add a site repeatedly. If a site has been connected by another account, you need to reclaim it through [site verification](https://intl.cloud.tencent.com/document/product/1145/45969).

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
3. Choose a service region and a plan as needed, tick the service agreement checkbox, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/6993099afd7680fc5d1b0e0f118b4f29.png)
 - Service region: <strong>Chinese mainland</strong>/<strong>Global (Chinese mainland not included)</strong>/<strong>Global</strong>. When it is set to "Chinese mainland" or "Global", make sure your domain name has an ICP filing.
 - Plan type: For more information about EdgeOne plans, see <a href="https://www.tencentcloud.com/document/product/1145/48705">Billing Overview</a>. If you want to activate the Enterprise plan, <a href="https://intl.cloud.tencent.com/contact-us">contact us</a>.
4. Select the NS access mode for your site. The existing DNS records will then be automatically scanned and imported. You can add/delete/modify the records and configure the [proxy mode](https://intl.cloud.tencent.com/document/product/1145/45968) as needed. Then, click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/895a7f8ba2f56c04087c44284ccc2053.png)
5. Log in at the domain registrar of your site and modify the NS server records to the value specified in EdgeOne as instructed on the NS server modification page. For detailed directions, see [How to Modify NS](#NSXG). 
![](https://qcloudimg.tencent-cloud.cn/raw/4cd54e76034647997567c54c3cca094d.png)
6. After modification, click **Complete** to redirect to the site overview page.
>? You will be notified via email, SMS, and Message Center when the changes take effect. The amount of time required depends on your domain registrar.

## CNAME Access
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Add site**.
![](https://qcloudimg.tencent-cloud.cn/raw/eee8acf7a9ce5b243cb4ec96961b8f4a.png)
2. On the site addition page, enter a valid second-level domain name and click **Next**.
>? You cannot add a site repeatedly. If a site has been connected by another account, you need to reclaim it through [site verification](https://intl.cloud.tencent.com/document/product/1145/45969).

![](https://qcloudimg.tencent-cloud.cn/raw/e3677f3738c1a65ea34fe413be154d01.png)
3. Choose a service region and a plan as needed, tick the service agreement checkbox, and click **Next**.
![](https://qcloudimg.tencent-cloud.cn/raw/250107793747b905f229a07680539a98.png)
 - Service region: <strong>Chinese mainland</strong>/<strong>Global (Chinese mainland not included)</strong>/<strong>Global</strong>. When it is set to "Chinese mainland" or "Global", make sure your domain name has an ICP filing.
 - Plan type: For more information about EdgeOne plans, see <a href="https://www.tencentcloud.com/document/product/1145/48705">Billing Overview</a>. If you want to activate the Enterprise plan, <a href="https://intl.cloud.tencent.com/contact-us">contact us</a>.
4. Select the CNAME access mode and click **Next**. 
![](https://qcloudimg.tencent-cloud.cn/raw/d96f126fbc9a240bac97baa882dbb631.png)
5. On the dialog that displays, [verify your site](https://intl.cloud.tencent.com/document/product/1145/45969) using a DNS record or file before clicking **Complete**.
![](https://qcloudimg.tencent-cloud.cn/raw/8627688759d94e3b6ff12f6c0b474b54.png)

## How to Modify NS[](id:NSXG)
1. Log in at the domain registrar of your site. If you cannot confirm the registrar, query it at [ICANN WHOIS](https://lookup.icann.org/).
2. After login, disable the Domain Name System Security Extensions (DNSSEC) configuration.
3. Delete the original NS configuration and modify it to the value specified in EdgeOne.
4. Wait for the NS records to take effect. You will be notified by email, Message Center, and SMS once they take effect.

Configuration guides for major domain registrars:
- [Amazon](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-name-servers-glue-records.html#domain-name-servers-glue-records-adding-changing)
- [GoDaddy](https://sg.godaddy.com/zh/help/change-nameservers-for-my-domains-664)
- [Google Domains](https://support.google.com/domains/answer/3290309?hl%3Den)
- [Name.com](https://www.name.com/support/articles/205934547-changing-nameservers-for-dns-management)
- [Yahoo!](http://support.hostgator.com/articles/how-to-change-name-servers-with-yahoo-com)