### How long is the default timeout for Tencent Cloud CDN nodes?
10 seconds.

### What will happen to the files on the CDN node if I close the connected domain from CDN management?
If you close the CDN service of a domain which has already been connected to CDN, the CDN node will retain the connection configurations of the domain, no further CDN traffic will be generated, and all requests towards this domain will be forwarded to the origin server. Before this operation, make sure that:
- You have configured the CNAME of this domain based on A record, otherwise the domain cannot be accessed.
- Your origin server has enough bandwidth processing capabilities, otherwise your domain name may not be accessed normally.

### What to do when I can't open my website after connecting to CDN?
First, check if the CDN status of the connected domain is "Closed". The website will not function if status is "Closed". Proceed the next step if the status is not "Closed":
+ Use ping or nslookup to check whether the CNAME resolution of the domain has taken effect. If CNAME is not added, please go to your DNS provider to add the CNAME as instructed by CNAME Configuration.
+ After CNAME takes effect, check if you can access the origin server normally.

If the problem is not solved after completion of the above procedure, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).

### How do I tell which CDN node are the users accessing?
You can acquire basic troubleshooting information such as the IP, latency and lost packet of the CDN node accessed by users by using the commands ping and nslookup.

### Why do I have a low hit rate?
This is generally caused by the following reasons:
+ Cache configuration problem, such as short cache validity period;
+ HTTP Header prevents caching. Check the origin server's Cache-Control or Expires configurations;
+ Few cacheable content for the origin server type;
+ Website has less visits and low validity period. Low hit rate for files leads to frequent origin-pull requests.

### 6. Users are experiencing a slow connection when accessing CDN?
We consider download speed for large files and latency for small files. First, acquire the URL that is slow to access for users and determine if the access is slow by using speed test websites.
If the connection is slow according to test and the origin server is a self-owned origin, you should assist the user to check if the machine load and bandwidth of the origin server are restricted.

### How do I tell whether a user access has hit the CDN Cache?
View the `X-Cache-Lookup` information in the header of the request return. If multiple `X-Cache-Lookup` entries are returned at the same time, that is normal. If `Hit From MemCache`/`Hit From Disktank` is returned, it means the CDN cache is hit.
![](https://mc.qcloudimg.com/static/img/64ac912c895b36f0241a927df6da3543/image.png)
+ X-Cache-Lookup:Hit From MemCache: Memory of the CDN node is hit.
+ X-Cache-Lookup:Hit From Disktank: Disk of the CDN node is hit.

### Why are the sizes of files with the same name returned by the node different?
As all file types are cached by default, there may be different versions for a file on the CDN node. To solve this problem:
+ Manually purge files and update cache immediately.
+ Use a version number, for example: ```http://www.xxx.com/xxx.js?version=1```.
+ Change the file name to avoid using files with the same name.

If the problem is not solved after completion of the above procedure, contact us by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).
