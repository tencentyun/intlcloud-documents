[](id:q1)
### How do I connect a domain name?
You can connect a domain name in the Content Delivery Network (CDN) console. For more information, see [Adding Domain Names](https://intl.cloud.tencent.com/document/product/228/5734).

[](id:q2)
### Are there any requirements for connecting a domain name to CDN?
1. The domain name cannot exceed 81 characters in length.
2. If the domain name requires acceleration in the Chinese mainland or global acceleration, you must obtain an ICP filing for the domain name from the Ministry of Industry and Information Technology (MIIT). If the domain name requires acceleration outside the Chinese mainland, you do not need to obtain an ICP filing for the domain name.
3. It takes 1 to 2 hours to synchronize ICP filing information. Re-add the domain name 1 or 2 hours after the ICP filing is complete.
4. The domain name can contain underscores (_) and Punycode-converted Chinese characters. You must obtain ICP filings for Chinese domain names before you convert the Chinese characters in the domain names to Punycode.
5. You can connect wildcard domain names in various formats, such as `*.example.com` and `*.a.example.com`. After you connect a wildcard domain name, its subdomain names or second-level wildcard domain names cannot be connected under another account. For example, if you connect the `*.example.com` wildcard domain name, the access traffic to the `a.example.com` domain name is accelerated based on the settings that are configured for the `*.example.com` wildcard domain name, whereas the access traffic to the `example.com` domain name is not accelerated.
6. You can connect multiple levels of nested domain names, such as `*.example.com`, `*.path.example.com`, and `a.path.example.com`, at the same time under an account. In this case, the domain name settings are applied and traffic statistics are calculated based on the priorities of the domain names. A more accurate match between the accessed domain name and a connected domain name indicates a higher priority for the connected domain name. For example, the access traffic to `a.path.example.com` is accelerated based on the settings of `a.path.example.com`, the access traffic to `b.path.example.com` is accelerated based on the settings of `*.path.example.com`, and the access traffic to `c.example.com` is accelerated based on the settings of `*.example.com`. The same analogy applies to traffic statistics.
7. If the subdomain names of a wildcard domain name are connected under other accounts, the wildcard domain name can be connected only after the subdomain names are disconnected under the accounts. For example, if the `a.example.com` subdomain name of the `*.example.com` wildcard domain name is connected under Account A, you must delete the subdomain name under Account A before you can connect the `*.example.com` wildcard domain name under Account B.

[](id:q3)
### Does CDN support connecting wildcard domain names?
Yes, CDN supports connecting wildcard domain names, for which domain name ownership verification is required. Once verified, domain names can be connected or retrieved.
In addition:
1. If a wildcard domain name such as `*.test.com` is already connected to Tencent Cloud, then none of its sub-domain names can be connected to another account.
2. If the `*.test.com` wildcard domain name is connected under the current account, wildcard domain names in a format such as `*.path.test.com` can be connected only under the current account.
3. If multiple levels of nested domain names are connected at the same time under an account, the domain name settings are applied and traffic statistics are calculated based on the priorities of the domain names. A more accurate match between the accessed domain name and a connected domain name indicates a higher priority for the connected domain name. For example, the access traffic to `a.path.test.com` is accelerated based on the settings of `a.path.test.com`, and the access traffic to `b.path.test.com` is accelerated based on the settings of `*.path.test.com`.


### Why do I get an error that the VOD domain name cannot be accessed?
It’s because your domain name has already been added to the VOD console. If you want to manage the domain name in the CDN console, it must be deleted from the VOD console and wait about 1 minute before adding it to the CDN console, or access other subdomain names.

[](id:q4)
### How long does it take to configure CDN?
Most CDN configurations take effect within 5 minutes. Some CDN configurations take effect within 5 to 15 minutes because a large number of tasks need to be run to complete the configurations. Please wait.

[](id:q5)
### Can I configure multiple origin server IPs?
Yes. After you configure multiple IPs, CDN will randomly access one of the IPs when forwarding a request to the origin server. If the number of origin-pull failures with this IP exceeds the threshold, the IP will be isolated for 300 seconds by default, during which no origin-pull requests will be forwarded to the IP.

[](id:q6)
### How do I bind CNAME to a domain name after the domain name is connected to CDN?
See [CNAME Configuration](https://www.tencentcloud.com/document/product/228/3121) for how to bind CNAME with your DNS service provider.

[](id:q13)
### What business types does CDN support?
The selected service type determines which resource platform is used by the domain name. Acceleration configurations vary by resource platforms. Please choose the service type that matches your business:
- Acceleration of small webpage file downloads: applicable to e-commerce, websites, UGC communities, and other business scenarios that mainly involve small static resources, such as webpage styles, images, and small files.
- Acceleration of large file downloads: applicable to business scenarios where large files, such as game installation packages, application updates, and application program packages, are downloaded.
- Audio and video on demand acceleration: applicable to audio and video on-demand scenarios that require acceleration, such as online on-demand audio and video streaming.
- Dynamic and static content acceleration: applicable to business scenarios where dynamic and static data is integrated, such as various website homepages.
- Dynamic content acceleration: applicable to scenarios such as account login, order transactions, API calls, and real-time queries.


### Why do exceptions such as old resources, old content, and incorrect content occur after the acceleration?
CDN nodes cache resources based on the [cache validity configuration](https://intl.cloud.tencent.com/document/product/228/38424). If the resources that are cached on a CDN node are not expired, the CDN node does not synchronize the latest resources from the origin server.
After a resource on the origin server is updated, its cache on the CDN node must be updated immediately. You can use the [cache purge](https://console.cloud.tencent.com/cdn/refresh) feature to update unexpired caches on the CDN node, so as to ensure that resources cached on the CDN node and stored on the origin server are consistent.


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
The origin domain is the website domain name that is accessed on the origin server during origin-pull on a CDN node. The IP or domain name that is configured on the origin server allows a CDN node to find the corresponding origin server during origin-pull. If multiple websites run on the origin server, the origin domain configuration specifies the domain name of the website to which requests are forwarded. If only one website runs on the origin server, you do not need to modify the origin domain, and the acceleration domain name is used as the origin domain by default.
If you use a Tencent Cloud Object Storage (COS) bucket or a bucket of a third-party object storage service as the origin server, you cannot modify the origin domain, and the origin-pull address is used as the origin domain by default.

[](id:q18)
### How do I tell whether CDN has taken effect?

1. View the domain name list in the CDN console. The CDN acceleration service has taken effect for your domain name if at least one CNAME resolution record is valid for the domain name. This means that the CNAME resolution of the domain name is complete.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/XPtc239_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224145315.png)
2. Alternatively, run the `nslookup` or `dig` command. In this example, the domain name is `www.test.com`.
	- If you use Windows, open the command prompt and run the `nslookup -qt=cname www.test.com` command. Check the CNAME resolution record in the output. If the CNAME resolution record is the same as the CNAME address that is provided by CDN, the CDN acceleration service has taken effect for the domain name.
	![](https://qcloudimg.tencent-cloud.cn/raw/5e862065b78633043f7cf1da228f6554.png)
	- If you use macOS or Linux, open the command prompt and run the `dig www.test.com` command. Check the CNAME resolution record in the output. If the CNAME resolution record is the same as the CNAME address that is provided by CDN, the CDN acceleration service has taken effect for the domain name.
	![](https://qcloudimg.tencent-cloud.cn/raw/0c1b07cd489d05f450297983df191d50.png)

[](id:q19)
### What do I do if files fail to be downloaded from CDN?

If files cannot be downloaded from CDN, we recommend troubleshooting by the following methods:
1. Check whether files can be downloaded normally from the origin server.
2. Check whether the domain name is correctly configured in the CDN console (see the origin domain in the **Basic Configuration** tab). Make sure that the configured origin domain name can be connected properly. Otherwise, origin-pull may fail, which will affect your business.
3. Check the security policy of the origin server. Check whether the origin-pull failure is caused by the security policy that is configured on the origin server. If so, obtain the intermediate IP range and add the origin server to the allowlist.

[](id:q20)
### What should I do if I cannot log in to the WordPress backend after CDN acceleration is configured?
When you configure CDN acceleration for WordPress, you must properly configure cache rules for resources that are related to dynamic requests, such as interface-related resources and login-related resources (resources in the /wp-admin backend login address). Otherwise, you may encounter a login failure. We recommend that you do not cache dynamic files.


### What do I do if the origin-pull protocol or port is invalid when I configure the origin server?

Tencent Cloud CDN supports port customization when you configure the origin server. If you set the origin-pull protocol to HTTP, port 80 is used for origin-pull by default. If you set the origin-pull protocol to HTTPS, port 443 is used for origin-pull by default. If you configure a custom port, the custom port is used for origin-pull. Make sure that you properly configure the origin-pull protocol and port when you configure the origin server. Otherwise, origin-pull may fail. The following examples list the common configuration errors:
1. The origin-pull protocol is set to HTTP, but the origin server supports only HTTPS-based origin-pulls.
2. The origin-pull protocol is set to HTTP, and the custom port 443 is used. However, the origin server supports only HTTPS-based origin-pulls.
3. The origin-pull protocol is set to HTTP, and the custom port 8080 is used. However, the origin server does not support access requests from port 8080.

If the origin-pull protocol is valid and the default port is invalid, use a custom port. After you enter the information about the origin server, the system automatically checks whether the origin server supports access from the custom port and returns the check result. If the check fails, troubleshoot issues based on the returned check result.

### Does CDN support .top domain names?
Yes. CDN already supports domain names suffixed with .pw or .top.


### Does CDN support Chinese domain names?
CDN supports domain names that contain underscores (_) and Punycode-converted Chinese characters.
- You must obtain ICP filings for Chinese domain names before you convert the Chinese characters in the domain names to Punycode.
- After you add a Chinese domain name, to the allowlist, you can convert the domain name to `xn--fiq228c.xn--eqrt2g` by using a thrid-party tool, and then connect `xn--fiq228c.xn--eqrt2g` to CDN.
- You can directly add domain names that contain underscores (_), such as `test_qq.tencent.cloud`.


### What will happen to the files on CDN nodes if I disable the connected domain name in the CDN console?
If you disable the CDN service of a connected domain name, CDN nodes will retain the connection configurations of the domain name, CDN traffic will no longer be generated, and the domain name will be inaccessible.


### Why does the “The CAM policy is not configured for the sub-account” error message appear?
The error message appears when you use a sub-account to perform operations, such as adding domain names and querying data, and you have not used the root account to attach policies to the sub-account. To resolve the problem, use the root account to go to the [Policies](https://console.cloud.tencent.com/cam/policy/createV3) page in the CAM console, create CDN-related policies, and attach the policies to the sub-account. After the authorization is complete, you can go to the [user list](https://console.cloud.tencent.com/cam) to view the policies that are attached to the sub-account.

### How do I disable or delete an acceleration domain name? Will the configuration be retained after the acceleration domain name is disabled or deleted?
To stop acceleration, log in to the CDN console, disable the domain name, and then delete the domain name. For more information, see [Domain Name Operations](https://intl.cloud.tencent.com/document/product/228/5736). If you cannot delete the domain name after you disable it, check whether the domain name is in the Disabling state. If not, check whether you are logged in to the CDN console with a sub-account. If yes, use the root account to grant the required permissions to the sub-account.
After a domain name is disabled, resources that have been configured are retained, but the acceleration stops and the 404 error code is returned for incoming user requests. After the domain name is deleted, resources that have been configured are immediately deleted and cannot be recovered.

### How do I enable CDN acceleration for the `example.com`, `www.example.com`, and `m.example.com` domain names at the same time?

1. To enable CDN acceleration for the three different domain names, connect them one by one to CDN. If you want to apply the same settings to the three domain names, add the domain name in batches or replicate the settings when you add the domain names.
2. To access the same resource from multiple domain names, such as `example.com` and `www.example.com`, add an implicit or explicit URL at your DNS provider to point the domain names to a website by using the 301 redirect technology. For more information, see [Implicit and Explicit URL Records](https://docs.dnspod.com/dns/implicit-explicit-url-records/?lang=en).

### Does CDN support a WebSocket connection?
We recommend that you enable dynamic and static content acceleration or dynamic content acceleration by using Enterprise Content Delivery Network (ECDN). You can configure the timeout period for the WebSocket connection. The timeout period can be up to 300 seconds. The WebSocket connection may be unstable or even fail when you use the following acceleration types: small webpage file downloads, large file downloads, and audio and video on demand.
