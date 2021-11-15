[](id:q1)
### What's node cache validity configuration?
Node cache validity configuration refers to a set of validity rules the CDN cache nodes should follow when caching your business contents.
All resources cached on CDN nodes have validity. For unexpired resources, when a request reaches the node, the node will directly return the requested resources to the user, so as to speed up the resource acquisition. For expired resources, the node will forward the user request to the origin server. If the resources have been updated on the origin server, they will be reacquired, cached to the node, and then returned to the user; otherwise, only the resource validity will be updated on the node. A proper cache validity can effectively improve the resource hit rate and lower the origin-pull rate, reducing bandwidth usage.


[](id:q2)
### How do I control the file cache validity in a browser?
You can configure the browser cache validity on the console. For more information, please see [Browser Cache Validity Configuration](https://intl.cloud.tencent.com/document/product/228/38932).

[](id:q3)
### I use my own server as the origin server of CDN. Can I configure CDN to not cache a specific type of files? Can I set the cache validity to "0" to disable caching?
You can configure different cache validity periods for different types of directories and files. If the cache validity is configured to "0", the CDN node will not cache the resource, in which case the CDN node needs to pull related resources from the origin server every time the users send access requests to the node. For more information on cache configurations, please see [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).

[](id:q4)
### What cache validity configuration does Tencent Cloud support?
Tencent Cloud CDN supports configuring cache actions and cache validity rules for various file types, and you can also adjust the priority of custom cache rules. Proper cache validity rules can effectively improve the resource hit rate and lower the origin-pull rate, reducing bandwidth usage. For more information, please see [Cache Configuration](https://intl.cloud.tencent.com/document/product/228/35316).

[](id:q5)
### What is the default cache configuration of CDN?
When adding an acceleration domain name, default node cache validity rules are added based on different acceleration service types and can be modified as needed.
- If static acceleration is selected, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached by default, and other files will be set to follow the origin server by default.
- If download or streaming VOD acceleration is selected, the default cache validity of all files will be 30 days.


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
