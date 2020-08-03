### How long is the default timeout period for Tencent Cloud CDN nodes?
10 seconds.

### What will happen to the files on the CDN node if I disable the connected domain name on the CDN Console?
If you disable the CDN service of a domain name that has already been connected to CDN, the CDN node will retain the connection configurations of the domain name, CDN traffic will no longer be generated, and all requests towards this domain name will be forwarded to the origin server. Before carrying out this operation, make sure that:
- You have configured the CNAME of this domain name based on A record. Otherwise, you will not be able to access the domain name.
- Your origin server has enough bandwidth processing capabilities. Otherwise, you may not be able to access your domain name.

### What should I do if I cannot open my website after connecting to CDN?
First, check whether the CDN status of the connected domain name is ""Disabled"". The website will not open if the status is ""Disabled"". Proceed to the next step if the status is not ""Disabled"":
+ Run `ping` or `nslookup` to check whether the CNAME resolution of the domain name has taken effect. If CNAME has not been added yet, please go to your DNS provider and add CNAME as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
+ After CNAME takes effect, check whether you can access the origin server as usual.

If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### How do I determine which CDN node is accessed by users?
By running the `ping` and `nslookup` commands, you can get basic troubleshooting information such as the IP, latency, and packet loss of the CDN node accessed by users.

### Why do I have a low hit rate?
This is generally due to the following reasons:
+ There is a cache configuration problem, such as a short cache validity period;
+ The HTTP header prevents caching. Check the origin server's `Cache-Control` or `Expires` configurations;
+ There are few cacheable contents for the origin server type;
+ The website has few visits and the validity period is short. The low hit rate for files leads to frequent origin-pull requests.

### Why do users experience a slow connection when they access CDN?
You should check the download speed for large files and the latency for small files. First, get the URL that is slow to access for users and determine whether the access is slow by using speed test websites such as [17ce](http://www.17ce.com) (recommended):
If the test connection is slow and the origin server is an external origin, you should assist the user and check if the machine load and bandwidth of the origin server are restricted.

### How do I tell whether a user access request has hit the CDN cache?
View the `X-Cache-Lookup` information in the header of the request return. If multiple `X-Cache-Lookup` entries are returned at the same time, that is normal. If `Hit From MemCache/Hit From Disktank` is returned, it means that the CDN cache has been hit.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)

+ X-Cache-Lookup:Hit From MemCache: the memory of the CDN node is hit.
+ X-Cache-Lookup:Hit From Disktank: the disk of the CDN node is hit.

### Why are the sizes of files with the same name returned by the node different?
Since all file types are cached by default, there may be different versions of a file on the CDN node. To solve this problem:
+ Manually purge files and update the cache immediately.
+ Use a version number, such as ```http://www.xxx.com/xxx.js?version=1```.
+ Change the file names to avoid using files with the same name.

If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.


### What should I do if my website cannot be accessed after the hotlink protection allowlist is configured in CDN?

Please select **Allow blank referer** when configuring the hotlink protection allowlist, so that the website can be opened normally in a browser (with a blank referer).
![](https://main.qcloudimg.com/raw/3ec77732d4f5266278af2e8f569b08a2.png)

### Can the traffic cap configuration defend against DDoS attacks?

CDN mainly focuses on content delivery acceleration rather than DDoS protection. You can use CDN’s bandwidth cap feature to automatically collect bandwidth usage statistics in 5 minutes. If the cap threshold is reached, CDN will respond according to the configuration. **The maximum threshold is 10,000 Tbps.**

### Can CDN provide all of its node IPs?
No. For security reasons, CDN cannot provide a full node IP list. However, you can query the IP region on the ""Verify Tencent Cloud CDN IP"" page. For more information, please see [Verify Tencent IP](https://intl.cloud.tencent.com/document/product/228/10747).
