### Does Tencent Cloud CDN have the acceleration capability on a global scale?
Tencent Cloud CDN supports global acceleration. Tencent has built nodes for over a decade, and Tencent Cloud CDN offers over 200 overseas nodes in more than 50 countries and regions to help your business go global seamlessly.

### Do changes need to be made on origin server for the acceleration service to take effect after CDN connection?
Basically, no change is needed. To achieve a better acceleration result, however, we recommend you assign static and dynamic files to different domain names and only accelerate static resources.

### Does Tencent Cloud CDN support cross-region access?
Tencent Cloud CDN does not have any cross-region access restrictions. If cross-region access is needed for your website, simply configure the Access-Control-Allow-Origin field in your website, or configure cross-region headers for your domain name in the CDN. For more information, please see [HTTP Header Configuration](https://intl.cloud.tencent.com/doc/product/228/6296).

### Where can I download the CDN access log?
You can download the CDN access log in the CDN Console. For more information, please see [Download Log](https://intl.cloud.tencent.com/document/product/228/6316#.E6.97.A5.E5.BF.97.E4.B8.8B.E8.BD.BD).

### How do I use the self troubleshooting tool?
The self troubleshooting tool provides a range of diagnostic features such as testing DNS, linkage quality, site availability and data access consistency for the access domain name. For more information, please see [Self Troubleshooting Tool](https://intl.cloud.tencent.com/document/product/228/6304). The tool is subject to the configuration of the local network environment and do not completely represent the entire network testing results.

### What is the difference between the local access diagnostics and the user access diagnostics?
Local access diagnostics: When you find an error with one of your resource accesses, you can initiate a test with the "local access diagnostics".
User access diagnostics: When your users report an error with resource access, you can pinpoint the problem via "user access diagnostics" and troubleshoot the problem following the instruction of Tencent Cloud.

### Does CDN support POST requests?
Yes. CDN supports POST requests.

### Does CDN support the origin server's cache-control configuration?
By default, Tencent Cloud CDN supports origin server's cache-control configuration.

### Does CDN support GZIP compression?
To help you save traffic, CDN compresses files with a size between 256 Byte and 2048 KB and a file name extension of .js, .html, .css, .xml, .json, .shtml, and .htm into Gzip files.

### Does CDN acceleration support ports other than 80?
CDN accelerator supports ports 80, 443 and 8080.

### What is a CDN intermediate server?
CDN intermediate server is a middle-layer origin-pull server located between the customer server and CDN node. The intermediate server converges the node's origin-pull requests to reduce the origin-pull pressure on your origin server.

### How do I obtain the real client IP?
After a request goes through an edge server, a `x-forward-for` header that includes the client’s real IP information will be added to the request.
