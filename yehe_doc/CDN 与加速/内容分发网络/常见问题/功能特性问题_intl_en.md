### Does Tencent Cloud CDN have the acceleration capability on a global scale?
Tencent Cloud CDN supports global acceleration. Tencent has built nodes for over a decade, and Tencent Cloud CDN offers over 1000 overseas nodes in more than 50 countries and regions to help your business go global seamlessly.

### Do changes need to be made on origin server for the acceleration service to take effect after CDN connection?
Basically, no change is needed. To achieve a better acceleration result, however, we recommend you assign static and dynamic files to different domain names and only accelerate static resources.

### Does Tencent Cloud CDN support cross-region access?
Tencent Cloud CDN does not have any cross-region access restrictions. If cross-region access is needed for your website, simply configure the Access-Control-Allow-Origin field in your website, or configure cross-region headers for your domain name in the CDN. For more information, please see [HTTP Header Configuration](https://intl.cloud.tencent.com/document/product/228/35320).

### Where can I download the CDN access log?
You can download CDN access logs in the CDN Console. For detailed directions, please see [Log Download](https://intl.cloud.tencent.com/document/product/228/6316),

### How do I use the self-diagnosis tool?
The self-diagnosis tool provides a range of diagnostic features such as testing DNS, linkage quality, site availability and data access consistency for the access domain name. For more information, please see [Self-Diagnosis Tool](https://intl.cloud.tencent.com/document/product/228/6304). The tool is subject to the configuration of the local network environment and do not completely represent the entire network testing results.

### What is the difference between the local access diagnosis and the user access diagnosis?
Local access diagnosis: when you find an error with one of your resource accesses, you can initiate a test with the "local access diagnosis".
User access diagnosis: when your users report an error with resource access, you can pinpoint the problem via "user access diagnosis" and troubleshoot the problem following the instruction of Tencent Cloud.

### Does CDN support POST requests?
Yes. CDN supports POST requests.

### Does CDN support the origin server's cache-control configuration?
By default, Tencent Cloud CDN supports origin server's cache-control configuration.

### Does CDN support gzip compression?
To help you save traffic, CDN compresses files with a size between 256 Byte and 2048 KB and a file name extension of .js, .html, .css, .xml, .json, .shtml, and .htm into gzip files.

### Does CDN acceleration support ports other than 80?
CDN accelerator supports ports 80, 443, and 8080.

### What is a CDN intermediate server?
CDN intermediate server is a middle-layer origin-pull server located between the customer server and CDN node. The intermediate server converges the node's origin-pull requests to reduce the origin-pull pressure on your origin server.

### How do I obtain the real client IP?
After a request goes through an edge server, a `x-forward-for` header that includes the client’s real IP information will be added to the request.

### How do I configure CDN sub-users?
Sub-users do not need to register for Tencent Cloud or activate the CDN service. They are added to the sub-user list by the creator. There are two types:
1. Message recipients.
2. Console users. For more information on how to create and configure a sub-user, please see [Creating Sub-User](https://intl.cloud.tencent.com/document/product/228/35229).

### How do I configure IP blacklist/whitelist in CDN?
CDN supports configuring IP blacklist/whitelist that enables you to create filtering policies for source IPs of user requests based on your business needs, helping prevent hotlinking and attacks from malicious IPs. For more information, please see [IP Blacklist/Whitelist Configuration](https://intl.cloud.tencent.com/document/product/228/6298).

For more information on the configuration, please see [IP Access Frequency Limit Configuration](https://intl.cloud.tencent.com/document/product/228/6420) and [Hotlink Protection Configuration](https://intl.cloud.tencent.com/document/product/228/6292).

### How do I configure Range Gets in CDN?
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to be edited. For more information, please see [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184). 
![](https://main.qcloudimg.com/raw/d3e75f57d7731cedbbc55690fccf8e42.png)
Click **Origin Configuration** and you will see the "Range GETs Configuration" module. ![](https://main.qcloudimg.com/raw/8a7e81c54c7cb0f950441759c0e62f48.png)

### Why can't CDN hide an IP completely?
1. The IP was already exposed before CDN is used.
2. The IP can still be perceived through technical means even after CDN is used.
3. There are multiple websites on the server, and if other domain names are not connected to CDN, the IP may be exposed.

### What does a hot backup origin server do?
If your primary origin server is an external one, you can add a hot backup origin server. All origin-pull requests will first be forwarded to the primary origin server. If a 4XX or 5XX error code is returned or an exception occurs such as link timeout or protocol incompatibility, requests will be forwarded to the hot backup origin server to pull resources, ensuring high availability of origin-pull.

### Does CDN support .top domain names?
CDN currently does not support domain names suffixed with .pw or .top.

### Is there a size limit for a file uploaded to CDN?
The maximum size of a file that can be uploaded to CDN is 32 MB by default.

### Does CDN support Chinese domain names?
CDN currently does not support Chinese domain names (even after transcoding).

### Can CDN forward requests to the origin server over the private network?
CDN currently can forward requests to the origin server only over the public network.
