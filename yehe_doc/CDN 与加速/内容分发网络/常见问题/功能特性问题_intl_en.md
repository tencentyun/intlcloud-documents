### Does Tencent Cloud CDN support global acceleration?
Yes. Tencent has been building nodes for over a decade. Tencent Cloud CDN offers over 1,000 overseas nodes in more than 50 countries and regions to help your business go global seamlessly.

### After connecting to CDN, do changes need to be made on the origin server for the acceleration service to take effect?
No. To achieve a better acceleration result, however, we recommend you assign static and dynamic files to different domain names and only accelerate static resources.

### Does Tencent Cloud CDN support cross-origin access?
Yes. If cross-origin access is needed for your website, simply configure the `Access-Control-Allow-Origin` field on your website or configure cross-origin headers for your domain name in the CDN Console. For more information, please see [HTTP Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320).

### Where can I download CDN access logs?
You can download CDN access logs in the CDN Console. For detailed directions, please see [Log Download](https://intl.cloud.tencent.com/document/product/228/6316).

### How do I use the CDN self-diagnosis tool?
The self-diagnosis tool provides a range of diagnostic features such as testing DNS, linkage quality, site availability, and data access consistency for the accessed domain name. For more information, please see [Self-Diagnosis Tool](https://intl.cloud.tencent.com/document/product/228/6304). The tool is subject to the configuration of the local network environment and do not fully represent the entire network testing results.

### What is the difference between the local access diagnosis and the user access diagnosis?
Local access diagnosis: when you find an exception with one of your resource accesses, you can initiate a test with "local access diagnosis".
User access diagnosis: when your users report an exception with their resource accesses, you can pinpoint the problem through "user access diagnosis" and troubleshoot the problem according to Tencent Cloud's suggestions.

### Does CDN support POST requests?
Yes.

### Does CDN support the origin server's Cache-Control configuration?
Yes. By default, CDN supports the origin server's `Cache-Control` configuration.

### Does CDN support gzip compression?
Yes. To help you save traffic, CDN compresses files between 256 bytes and 2,048 KB with filename extensions of .js, .html, .css, .xml, .json, .shtml, and .htm into gzip files.

### Does CDN acceleration support ports other than 80?
Yes. CDN acceleration supports ports 80, 443, and 8080.

### What is a CDN intermediate server?
A CDN intermediate server is a middle-layer origin-pull server located between the business server and the CDN node. The intermediate server converges the node's origin-pull requests to reduce the origin-pull pressure on your origin server.

### How do I obtain the real client IP?
After a request goes through an edge server, a `x-forward-for` header that includes the client's real IP information will be added to the request.

### How do I configure CDN sub-users?
Sub-users do not need to register for Tencent Cloud or activate the CDN service. They are added to the sub-user list by the creator. There are two types of sub-users:
1. Message recipients.
2. Console users. For more information on how to create and configure a sub-user, please see [Console Permissions](https://intl.cloud.tencent.com/document/product/228/35229).

### How do I configure an IP blocklist/allowlist in CDN?
CDN supports IP blocklist/allowlist configuration. You can create filtering policies for source IPs of user requests based on your business needs, helping prevent hotlinking and attacks from malicious IPs. For more information, please see [IP Blocklist/Allowlist Configuration](https://intl.cloud.tencent.com/document/product/228/6298).

For more information on this configuration, please see [IP Access Limit Configuration](https://intl.cloud.tencent.com/document/product/228/6420) and [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292).

### How do I configure Range GETs in CDN?
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name you want to edit. For more information, please see [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184). 
![](https://main.qcloudimg.com/raw/af642b65bed86a97fadaf229e26aceac.png)
Click **Origin Configuration** and you will see the "Range GETs Configuration" module. ![](https://main.qcloudimg.com/raw/79d08718f1399b735b9b2dc804bf383e.png)

### Why can't CDN hide an IP completely?
1. The IP was already exposed before CDN was used.
2. The IP can still be perceived through technical means even after CDN is used.
3. There are multiple websites on the server, and if other domain names are not connected to CDN, the IP may be exposed.

### What does a hot backup origin server do?
If your primary origin server is an external one, you can add a hot backup origin server. All origin-pull requests will be forwarded to the primary origin server first. If a 4XX or 5XX error code is returned or an exception such as connection timeout or protocol incompatibility occurs, requests will be forwarded to the hot backup origin server to pull resources, ensuring high availability of origin-pull.

### Does CDN support .top domain names?
No. Currently, CDN does not support domain names suffixed with .pw or .top.

### Is there a size limit for a file uploaded to CDN?
Yes. The maximum size of a file that can be uploaded to CDN is 32 MB by default.

### Does CDN support Chinese domain names?
No. Currently, CDN does not support Chinese domain names (even after transcoding).

### Can CDN forward requests to the origin server over the private network?
No. Currently, CDN can only forward requests to the origin server over the public network.

### Does CDN support using scripts to programmatically implement configuration?
Yes. CDN currently uses Lua scripts to programmatically implement configurations. These scripts are generally used for customization and written and released by the CDN technical support team

### Does CDN support configuring different origin servers for different client requests?
Yes. CDN supports origin-pull to different origin servers for different client requests. You can submit a description of your specific requirements, and the CDN technical support team will configure it for you on the backend.

### Does CDN support dynamic origin-pull configuration and origin-pull queuing?
If the primary origin server returns an exception, requests can be sequentially redirected to configured backup servers.
