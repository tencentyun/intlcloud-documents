[](id:q1)
### How do I add a domain name?
You can connect a domain name on the CDN console. For more information, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

[](id:q2)
### Are there any requirements for connecting a domain name to CDN?
Yes. The following are the requirements for connecting a domain name to CDN:
1. The length of the domain name cannot exceed 50 characters. Domain names in Chinese, even after they are transcoded, are not supported currently.
2. If the Chinese mainland CDN is used, the domain name must have an ICP filing issued by the MIIT, and the business content of the origin server must be legal.
3. The domain name is a sub-domain name in the format of `a.test.com` or `a.b.test.com` or a wildcard domain name in the format of `*.test.com` or `*.a.test.com`.
4. Domain name ownership verification is required when connecting a domain name for the first time, a wildcard domain name, or a connected domain name.

[](id:q3)
### Does CDN support connecting wildcard domain names?
Yes, CDN supports connecting wildcard domain names, for which domain name ownership verification is required. Once verified, domain names can be connected or retrieved.
In addition:
1. If a wildcard domain name such as `*.test.com` is already connected to Tencent Cloud, then none of its sub-domain names can be connected Tencent Cloud by other accounts.
2. If the wildcard domain name `*.test.com` is already connected to Tencent Cloud by your account, then wildcard domain names in formats such as `*.path.test.com` cannot be connected Tencent Cloud by your account.

[](id:q4)
### How long does it for the CDN configuration to take effect?
Generally, it takes less than 30 minutes for the CDN configuration to take effect. If the configuration does not take effect within 30 minutes, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

[](id:q5)
### Can I configure multiple origin server IPs?
Yes. After you configure multiple IPs, CDN will randomly access one of the IPs when forwarding a request to the origin server. If the number of origin-pull failures with this IP exceeds the threshold, the IP will be isolated for 300 seconds by default, during which no origin-pull requests will be forwarded to the IP.

[](id:q6)
### How do I bind CNAME to a domain name after the domain name is connected to CDN?
See [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.

[](id:q7)
### I can only disable a domain name but cannot delete it.
Please check whether the user is a collaborator. The collaborator needs to get the relevant permission from the creator for the operation. If you are sure that the collaborator has been granted the permission but still cannot perform the operation, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

[](id:q8)
### Will the domain name configuration be retained after the acceleration service is disabled?
Yes. After the acceleration service is disabled, the domain name configuration will be retained, but the acceleration service will no longer be available. A 404 status code will be returned for user requests.

[](id:q9)
### Will the domain name configuration be retained after an acceleration domain name is deleted?
No. After a domain name is deleted, its configuration will not be retained.

[](id:q10)
### How do I disable the acceleration service?
You can disable the acceleration service on the CDN console. For detailed directions, please see "Disabling the acceleration service" in [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q11)
### How do I delete an acceleration domain name?
You can delete an acceleration domain name on the CDN console. For detailed directions, please see "Deleting acceleration domain names" in [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).

[](id:q12)
### How do I unblock a domain name?
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

[](id:q13)
### What business types does CDN support?
The selected service type determines which resource platform is used by the domain name. Acceleration configurations vary by resource platforms. Please choose the service type that matches your business:
- Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
- Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
- Streaming VOD acceleration: Suitable for application scenarios such as audio/video VOD acceleration.

[](id:q14)
### How do I modify the project of a domain name in CDN?

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name, open the **Basic Configuration** tab, and then modify the domain name project. To modify the projects of multiple domain names in batches, please tick target domain names on the **Domain Management** page, click **More Actions** drop-down list, and select **Edit Project**. Up to 50 domain names can be operated at a time.

>!Users on the CDN permission system should proceed with caution, since this operation may cause changes to the permissions of sub-users.


[](id:m1)
### My domain name has already obtained an ICP filing from the MIIT. Why does the system prompt that it does not have an ICP filing when I try to connect it to CDN?
After you obtain your ICP filing, it takes some time to sync the information from the MIIT to Tencent Cloud CDN. Please wait 24 hours and try again.

[](id:q16)
### Can I configure ports for acceleration domain names or origin servers?
- CDN acceleration domain name port: currently, CDN acceleration ports can only be 80, 443, and 8080.
- Origin server port: the ports 1 to 65535 can be configured after the origin server address.

[](id:q17)
### What is CDN origin domain configuration?
Origin domain is the website domain name accessed on the origin server during origin-pull on a CDN node. Origin server and origin domain: The IP or domain name configured at the origin server allows a CDN node to find the corresponding origin server during origin-pull. There can be multiple websites on the server, and the origin domain indicates on which website a resource resides.

[](id:q18)
### How do I tell whether CDN has taken effect?

You can run the `nslookup` command to query the DNS resolution of your CDN acceleration domain name. If the resolution result domain name is suffixed with `dnsv1.com` (the CNAME record) as shown in the image, it indicates that the CDN acceleration service for your domain name has taken effect.
![](https://main.qcloudimg.com/raw/4576b46fd8a04b726e6893a08f3fe61f.png)


[](id:q19)
### What should I do if files cannot be downloaded from CDN?

If files cannot be downloaded from CDN, we recommend troubleshooting by the following methods:
1. Check whether files can be downloaded normally from the origin server.
2. Check whether the domain name is correctly configured on the CDN console (see the origin domain in the **Basic Configuration** tab). Please make sure that the configured origin domain can be accessed properly. Otherwise, origin-pull may fail, which will affect your business.
3. Check the security policy of the origin server. Please check whether the origin-pull failure is caused by the security policy configured on the origin server, and if so, please [contact us](https://intl.cloud.tencent.com/support) to get the intermediate IP range and add the origin server to the allowlist.

[](id:q20)
### What should I do if I cannot log in to the WordPress backend after CDN acceleration is configured?
WordPress involves dynamic requests. If the cache configuration is inappropriate, login exceptions may occur. We recommend setting the cache validity of the corresponding dynamic file type to 0, so that files of this type will not be automatically cached. Common dynamic file types include .asp, .jsp, .php, .perl, and .cgi. For detailed directions, please see [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).


