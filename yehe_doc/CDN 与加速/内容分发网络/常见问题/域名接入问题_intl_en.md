### How do I connect a domain name?
You can connect a domain name on the CDN Console. For more information, please see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

### Does CDN support connecting wildcard domain names?
Yes. CDN supports connecting wildcard domain names, but verification is needed. Upload the verification files provided by Tencent Cloud to the root directory of the website, and establish the connection to the wildcard domain name after the verification is completed successfully.
In addition:
1. If a wildcard domain name such as `*.test.com` is already connected to Tencent Cloud, then none of its sub-domain names can be connected to another account.
2. If the wildcard domain name `*.test.com` is already connected to your account, then wildcard domain names in formats such as `*.path.test.com` cannot be connected to your account.

### How long does it take to configure CDN?
Generally, it takes less than 30 minutes for the CDN configuration to take effect. If the configuration does not take effect within 30 minutes after configuration, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Are there any requirements for connecting a domain name to CDN?
Yes. Before a domain name is connected to CDN for acceleration, an ICP filing for services in Mainland China should have been obtained from the MIIT for the domain name, and the business contents on the origin server must be legally compliant.

### Can I configure multiple origin server IPs?
Yes. After you configure multiple IPs, CDN will randomly access one of the IPs when forwarding a request to the origin server. If the number of origin-pull failures with this IP exceeds the threshold, it will be isolated for 300 seconds by default and will no longer be used for origin-pull.

### How do I bind CNAME to a domain name after the domain name is connected to CDN?
Please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.

### Why can a domain name be disabled but not deleted?
Please check whether the user is a collaborator. The collaborator's permission is configured by the creator of the CDN service. If the creator does not assign the relevant permission to the collaborator, the collaborator cannot perform the operation. If you are sure that the collaborator has been granted the permission but still cannot perform the operation, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Will the domain name configuration be retained after the acceleration service is disabled?
Yes. After the acceleration service is disabled, the domain name configuration will be retained, but the acceleration service will no longer be available. In this case, any user requests will be forwarded to the origin server for origin-pull.

### Will the domain name configuration be retained after an acceleration domain name is deleted?
No. After the domain name is deleted, its configuration will not be retained.

### How do I disable the acceleration service?
You can disable the acceleration service on the CDN Console. For detailed directions, please see [Disabling an Acceleration Service](https://intl.cloud.tencent.com/document/product/228/5736).

### How do I delete an acceleration domain name?
You can delete an acceleration domain name on the CDN Console. For detailed directions, please see [Deleting an Acceleration Domain Name](https://intl.cloud.tencent.com/document/product/228/5736).

### How do I unblock a domain name?
Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### What business types does CDN support?
The business type determines the resource platform to be scheduled by the domain name. The acceleration configuration varies by resource platform. Please select a business type based on your business conditions:
- Static acceleration: suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
- Download acceleration: suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
- Streaming VOD acceleration: suitable for audio/video on demand acceleration scenarios.

### How do I modify the project of a CDN domain name?

1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name you want to edit.
![](https://main.qcloudimg.com/raw/fb85a5afb49ca90cfe0c6c9b075a5646.png)
2. Click the **Basic Configuration** tab to see the basic information module, where you can view the basic information of the domain name, including the project. **For users using the CDN permission system, please perform this operation carefully, as it may change the permissions of sub-users.**
3. Click **Modify** on the right of the project and select a new project in the drop-down list.
![](https://main.qcloudimg.com/raw/f788084a71b205ee8938c960edfb3a29.png)

You can also manage your projects on the [Project Management](https://console.cloud.tencent.com/project) page.


### Are there any requirements for connecting a domain name to CDN?
Yes. The following are the requirements for connecting a domain name to CDN:
1. The domain name can contain up to 50 characters. CDN currently does not support Chinese domain names (even after transcoding).
2. If Mainland China CDN is used, the domain name must have an ICP filing issued by the MIIT.
3. The domain name is a sub-domain name in the format of `a.test.com` or `a.b.test.com` or a wildcard domain name in the format of `*.test.com` or `*.a.test.com`.
4. If the domain name is a wildcard one or has been connected by another user, you need to [verify your ownership](https://intl.cloud.tencent.com/document/product/228/5734#m1) before connecting or retrieving it.

### My domain name has already obtained an ICP filing from the MIIT. Why does the system prompt that it does not have an ICP filing when I try to connect it to CDN?
After you obtain your ICP filing, it takes some time to sync the information from the MIIT to Tencent Cloud CDN. Please wait for 24 hours and try again.

### Can I configure ports for acceleration domain names/origin servers?
- CDN acceleration domain name port: currently, CDN acceleration ports can only be 80, 443, and 8080 by default.
- Origin server port: ports in the range of 1–65535 can be configured after the origin server address.

### What is CDN origin domain configuration?
Origin domain is the website domain name accessed on the origin server during origin-pull on a CDN node. Origin server and origin domain: the IP/domain name configured on the origin server allows the CDN node to find the corresponding origin server during origin-pull. There can be multiple websites on the server, and the origin domain indicates on which website the resource resides.


### How do I tell whether CDN has taken effect?

Ping the domain name and view the returned result. If `cdntip.com`and `ovscdns.com` are displayed in the returned result, CDN connection has succeeded.
### What should I do if files cannot be downloaded from CDN?

If files cannot be downloaded from CDN, we recommend you troubleshoot using the following methods:
1. Check whether files can be downloaded normally from the origin server.
2. Check whether the CDN domain name is correctly configured on the CDN Console > Basic Configuration > Origin Domain. Please make sure that the configured origin domain can be accessed properly. Otherwise, origin-pull may fail, which will affect your business.
3. Check the security policy of the origin server. Please check whether the origin-pull failure is caused by the security policy configured on the origin server. If so, please contact us to get the intermediate IP range and allowlist the origin server.


### What should I do if I cannot log in to the WordPress backend after CDN acceleration is configured?
WordPress involves dynamic requests. If the cache is configured inappropriately, login exceptions may occur. We recommend you set the cache expiration time of the corresponding dynamic file type to 0, so that files of this type will not be automatically cached. Common dynamic file types include .asp, .jsp, .php, .perl, and .cgi. For detailed directions, please see [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/35317).
