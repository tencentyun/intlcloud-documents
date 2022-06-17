[](id:q1)
### What's node cache validity configuration?
Node cache validity configuration refers to a set of validity rules the CDN cache nodes should follow when caching your business contents.
All resources cached on CDN nodes have validity. For unexpired resources, when a request reaches the node, the node will directly return the requested resources to the user, so as to speed up the resource acquisition. For expired resources, the node will forward the user request to the origin server. If the resources have been updated on the origin server, they will be reacquired, cached to the node, and then returned to the user; otherwise, only the resource validity will be updated on the node. A proper cache validity can effectively improve the resource hit rate and lower the origin-pull rate, reducing bandwidth usage.

[](id:q2)
### How do I control the file cache validity in a browser?
You can configure the browser cache validity on the console. For more information, please see [Browser Cache Validity Configuration](https://intl.cloud.tencent.com/document/product/228/38932).

[](id:q3)
### How do I configure CDN to return specific files without caching?
You can configure the cache validity for resources based on the directory, file path, file type. For more information, see [Node Cache Validity Configuration (New)](https://intl.cloud.tencent.com/document/product/228/38424).
When you set "No Cache" for a file, the file will not be cached on CDN nodes. Each time you request the file, CDN nodes will pull it from the origin server directly. 
![]()

[](id:q4)
### What cache validity configurations supported in CDN?
CDN allows you to set a cache validity period and whether to ignore query string, ignore case, follow origin server and enable heuristic cache for various file types. By using these cache rules properly, you can effectively improve the hit rate with a lower origin-pull rate and bandwidth usage. For details, see [Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35315) and [Node Cache Validity Configuration (New)](https://intl.cloud.tencent.com/document/product/228/38424).

[](id:q5)
### What is the default cache configuration of CDN?
When adding an acceleration domain name, default node cache validity rules are added based on different acceleration service types and can be modified as needed.
- The following types of resources are not cached by default, including CDN webpage files, large files and audio and video on demand, and ECDN dynamic and static content (such as PHP, JSP, ASP and ASPX dynamic files). Other files are cached for 30 days.
- For ECDN dynamic content acceleration, all files are not cached.

If no rule is configured or matches requests, the default policies will be applied:
- When a user makes a request for a certain business resource, if the HTTP response header of the origin server contains the field `Cache-Control`, the `Cache-Control` will be followed.
- If the HTTP response header of the origin server does not contain the field `Cache-Control`, then the resource cache validity on nodes will be 600 seconds.

[](id:q6)
### What are cache matching rules?
When multiple cache rules are set, the ones at the bottom of the list have higher priority. For example, if a domain name is configured as follows:
```
All files - 30 days
.php .jsp .aspx - 0 seconds
.jpg .png .gif - 300 seconds
/test/*.jpg - 400 seconds
/test/abc.jpg - 200 seconds
```

If the domain name is `www.test.com`, and the resource is `www.test.com/test/abc.jpg`, the matching rule will be as follows:
1. Match with the first rule. It is hit, so the cache validity is 30 days.
2. Match with the second rule. It is not hit.
3. Match with the third rule. It is hit, so the cache validity is 300 seconds.
4. Match with the fourth rule. It is hit, so the cache validity is 400 seconds.
5. Match with the fifth rule. It is hit, so the cache validity is 200 seconds.

The final cache validity is subject to the last matching result, so it will be 200 seconds.


### How do I tell whether user access has hit the CDN cache?
You can check the X-Cache-Lookup of the HTTP response header.
![](https://qcloudimg.tencent-cloud.cn/raw/4c8b8e2954bacadd520c94e6fa4aff31.png)
X-Cache-Lookup: Hit From MemCache
X-Cache-Lookup: Hit From Disktank
X-Cache-Lookup: Cache Hit
If any of the above is returned, a cache hit occurs, otherwise it is a cache miss.

### If the file changes on the origin server, will the cache on CDN cache nodes be updated in real time?
No. The cache on CDN cache nodes will not be updated in real time.
- CDN cache nodes update the cache according to the [cache validity configuration](https://intl.cloud.tencent.com/document/product/228/35317) rules you configure in the console. If there are file changes on the origin server and the cache is still valid, CDN cache nodes will not perform origin-pull to update the cache. As a result, the file on the origin server is different from the cache.
- If you need to update the cache of a file, you can [purge the cache](https://intl.cloud.tencent.com/document/product/228/6299). When you request the file, CDN will perform origin-pull to get the latest one and re-cache it. You can also [prefetch the cache](https://intl.cloud.tencent.com/document/product/228/39000) so that CDN pulls the latest resource from the origin server.
- If you need to update the cache of a file regularly, you can enable scheduled purge and prefetch and create a scheduled purge task.
