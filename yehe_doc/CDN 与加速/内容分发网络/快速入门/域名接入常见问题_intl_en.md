### How do I add a domain name?
You can connect a domain name on the CDN console. For more information, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

### Are there any requirements for connecting a domain name to CDN?
Yes. The following are the requirements for connecting a domain name to CDN:
1. The length of the domain name cannot exceed 50 characters. Domain names in Chinese, even after they are transcoded, are not supported currently.
2. If the Chinese mainland CDN is used, the domain name must have an ICP filing issued by the MIIT, and the business content of the origin server must be legal.
3. The domain name is a sub-domain name in the format of `a.test.com` or `a.b.test.com` or a wildcard domain name in the format of `*.test.com` or `*.a.test.com`.
4. If the domain name is a wildcard one or has been connected by another user, you need to [verify your ownership](https://intl.cloud.tencent.com/document/product/228/5734#m1) before connecting or retrieving it.

### Does CDN support connecting to wildcard domain names?
Yes. CDN supports connecting to wildcard domain names, but verification is needed. Upload the verification files provided by Tencent Cloud to the root directory of the website, and establish the connection to the wildcard domain name after the verification is completed successfully.
In addition:
1. If a wildcard domain name such as `*.test.com` is already connected to Tencent Cloud, then none of its sub-domain names can be connected to another account.
2. If the wildcard domain name `*.test.com` is already connected to your account, then wildcard domain names in formats such as `*.path.test.com` cannot be connected to your account.

### How long does it take to configure CDN?
Generally, it takes less than 30 minutes for the CDN configuration to take effect. If the configuration does not take effect within 30 minutes after configuration, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Can I configure multiple origin server IPs?
Yes. After you configure multiple IPs, CDN will randomly access one of the IPs when forwarding a request to the origin server. If the number of origin-pull failures with this IP exceeds the threshold, it will be isolated for 300 seconds by default and will no longer be used for origin-pull.

### How do I bind CNAME to a domain name after the domain name is connected to CDN?
See [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.

### Why can a domain name be disabled but not deleted?
Please check whether the user is a collaborator. The collaborator's permission is configured by the creator of the CDN service. If the creator does not assign the relevant permission to the collaborator, the collaborator cannot perform the operation. If you are sure that the collaborator has been granted the permission but still cannot perform the operation, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Will the domain name configuration be retained after the acceleration service is disabled?
Yes. After the acceleration service is disabled, the domain name configuration will be retained, but the acceleration service will no longer be available. In this case, a 404 status code will be returned for user requests.

### Will the domain name configuration be retained after an acceleration domain name is deleted?
No. After the domain name is deleted, its configuration will not be retained.

### How do I disable the acceleration service?
You can disable the acceleration service on the CDN console. For detailed directions, please see “Disabling the acceleration service” in [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).

### How do I delete an accelerated domain name?
You can delete an acceleration domain name on the CDN console. For detailed directions, please see “Deleting an acceleration domain name” in [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736).

### How do I unblock a domain name?
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### What business types does CDN support?
The selected service type determines which resource platform is used by the domain name. Acceleration configurations vary by resource platforms. Please choose the service type that matches your business:
- Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
- Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
- Streaming Media VOD acceleration: Suitable for application scenarios such as audio/video VOD acceleration.

### How do I modify the project of a CDN domain name?

1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name you want to edit.
![Image description](https://main.qcloudimg.com/raw/d2d85c86bca9c60c7e5ae5667fd2e155.png)
2. Click the **Basic Configuration** tab to see the basic information module, where you can view the basic information of the domain name, including the project. **For users using the CDN permission system, please perform this operation carefully, as it may change the permissions of sub-users.**
3. Click **Modify** on the right of the project and select a new project in the drop-down list. Then, click **OK**.
![Image description](https://main.qcloudimg.com/raw/1a2a312352d3353317075696347e0f42.png)

You can also manage your projects on the [Project Management](https://console.cloud.tencent.com/project) page.

<span ID = m1></span>
### My domain name has already obtained an ICP filing from the MIIT. Why does the system prompt that it does not have an ICP filing when I try to connect it to CDN?
After you obtain your ICP filing, it takes some time to sync the information from the MIIT to Tencent Cloud CDN. Please wait 24 hours and try again.

### Can I configure ports for acceleration domain names/origin servers?
- CDN acceleration domain name port: currently, CDN acceleration ports can only be 80, 443, and 8080 by default.
- Origin server port: ports in the range of 1–65535 can be configured after the origin server address.

### What is CDN origin domain configuration?
Origin domain is the website domain name accessed on the origin server during origin-pull on a CDN node. Origin server and origin domain: The IP/domain name configured at the origin server allows a CDN node to find the corresponding origin server during origin-pull. There can be multiple websites on the server, and the origin domain indicates on which website a resource resides.


### How do I tell whether CDN has taken effect?

Ping the domain name and view the returned result. If `cdntip.com` or `ovscdns.com` is displayed in the returned result, the CDN connection has succeeded.
![Image description](https://main.qcloudimg.com/raw/657d4b219f99acc10b55cf9faabd9943.png)
>? Since CDN has many nodes across regions, the IPs pointed to by the domain name connected to CDN vary during pings, which is normal.

### What should I do if files cannot be downloaded from CDN?

If files cannot be downloaded from CDN, we recommend you troubleshoot using the following methods:
1. Check whether files can be downloaded normally from the origin server.
2. Check whether the CDN domain name is correctly configured on the CDN console > Basic Configuration > Origin Domain. Please make sure that the configured origin domain can be accessed properly. Otherwise, origin-pull may fail, which will affect your business.
3. Check the security policy of the origin server. Please check whether the origin-pull failure is caused by the security policy configured on the origin server, and if so, please [contact us](https://intl.cloud.tencent.com/support) to get the intermediate IP range and allowlist the origin server.


### What should I do if I cannot log in to the WordPress backend after CDN acceleration is configured?
WordPress involves dynamic requests. If the cache is configured inappropriately, login exceptions may occur. We recommend you set the cache expiration time of the corresponding dynamic file type to 0, so that files of this type will not be automatically cached. Common dynamic file types include .asp, .jsp, .php, .perl, and .cgi. For detailed directions, please see [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/35317).


