### What is cache expiration configuration?
Cache expiration configuration refers to a set of expiration policies the CDN cache nodes should follow when caching your business contents.
All resources cached on CDN nodes have an expiration time. For resources in normal status, when a request reaches the node, the node will directly return the requested resource to the user, so as to speed up the resource acquisition. For expired resources, the node will forward the user request to the origin server, reacquire the resource and cache it to the node, and then return it to the user. A reasonable cache validity period can effectively improve the resource hit rate and lower the origin-pull rate, reducing bandwidth usage.


### How do I control the file cache time in a browser?
Tencent Cloud CDN supports the Cache-Control configuration on the origin server by default, but configuration of the Cache-Control header is not supported. Max-age cannot be configured on CDN nodes, but CDN nodes can inherit the origin server's max-age. To configure max-age on CDN nodes, you only need to configure the max-age on the origin server.

### How do I adjust the priority of cache configuration?
For more information, see [Priority Adjustment](https://intl.cloud.tencent.com/document/product/228/6290#.E4.BC.98.E5.85.88.E7.BA.A7).

### I use my own server as the origin server of CDN. Can I configure to not cache a specific type of files? Can I set the cache period to “0” to disable caching?
You can configure different cache validity periods for different types of directories and files. If the cache validity period is configured to 0, the CDN node will not cache the resource, in which case the CDN node needs to pull related resources from the origin server every time the users send access request to the node. For more information on cache configurations, see [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290).

### Which cache expiration configuration does Tencent Cloud support?
Tencent Cloud CDN supports cache validity period configuration at various dimensions, custom priority adjustment, and cache inheritance policies (advanced cache configuration). A reasonable cache validity period can effectively improve the resource hit rate and lower origin-pull rate, reducing bandwidth usage.

### What is the default cache configuration of CDN?
Default configuration is as follows when a domain is connected:
- Own origin domain connection: By default, the cache validity period for all files is 30 days, except general dynamic files (such as .php, .jsp, .asp, .aspx), for which the cache validity period is 0 by default, which means any request for such files will be directly forwarded to the origin server.
- COS origin domain connection: By default, the cache validity period for all files is 30 days;
- Advanced cache expiration configuration is disabled by default.

### What are cache inheritance policies?
When a user makes a request for a certain business resource, the origin server's Response HTTP Header includes the Cache-Control field. The default policy is as follows:
- If the Cache-Control field is `max-age`, the cache validity period for this resource is subject to the one set for the resource, instead of inheriting the value specified by `max-age`.
- If the Cache-Control field is `no-cache` or `no-store`, the CDN node does not cache the resource.

### What are cache matching rules?
When multiple caching policies are set, the priorities of the entries are determined on a bottom-to-top basis, with the entry at the bottom of list having the highest priority and the one at the top having the lowest priority. For example, if the following caching policies are set for a domain:
```
All files (30 days)
.php .jsp .aspx 0 seconds
.jpg .png .gif 300 seconds
/test/*.jpg 400 seconds
/test/abc.jpg 200 seconds
```

If the domain is `www.test.com`, and the resource is `www.test.com/test/abc.jpg`, the matching rule will be as follows:
1. Match with the first entry. It is hit, so the cache validity period is 30 days.
2. Match with the second entry. It is not hit.
3. Match with the third entry. It is hit, so the cache validity period is 300 seconds.
4. Match with the fourth entry. It is hit, so the cache validity period is 400 seconds.
5. Match with the fifth entry. It is hit, so the cache validity period is 200 seconds.

The final cache validity period is subject to the last matching result, 200 seconds.
