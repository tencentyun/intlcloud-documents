### What is cache validity configuration?
Cache validity configuration refers to a set of expiration policies the CDN cache nodes should follow when caching your business contents.
All resources cached on CDN nodes have an expiration time. For unexpired resources, when a request reaches the node, the node will directly return the requested resource to the user, so as to speed up the resource acquisition. For expired resources, the node will forward the user request to the origin server to reacquire the resource, and then cache it to the node and return it to the user at the same time. A reasonable cache validity period can effectively improve the resource hit rate and lower the origin-pull rate, reducing bandwidth usage.

### What is the advanced cache validity configuration?
1. Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Click **Manage** on the right of the target domain name.
![](https://main.qcloudimg.com/raw/53c1171f8b1fdec4ddd2f87f6c47fe12.png)
3. Open the **Cache Configuration** tab, find the **Node Cache Validity Configuration** section, and toggle on the **Advanced Cache Validity Configuration** switch.
![](https://main.qcloudimg.com/raw/b1288410345c3dd92907002ad5929d38.png)
4. The following results are then achieved.
When a user requests for a certain resource from the origin server and the response HTTP header includes the `Cache-Control` field with a value of `max-age=xxxx`, the cache validity period for the resource on the node will be the smaller one among the set validity period and the `max-age` value:
 - For example, if the `max-age` set for the `/index.html` of the origin server is 200 seconds and the cache validity period set for CDN is 600 seconds, the actual cache validity period for the file will be 200 seconds.
 - If the `max-age` set for the `/index.html` of the origin server is 800 seconds and the cache validity period set for CDN is 600 seconds, the actual cache validity period for the file will be 600 seconds.

>! If the `Cache-Control` field does not exist in the response header of your origin server, CDN adds the `Cache-Control: max-age=600` header by default.

### How do I control the file cache validity in a browser?
You can configure browser cache validity in the CDN console. For more information, please see [Browser Cache Validity Configuration](https://intl.cloud.tencent.com/document/product/228/38932).

### How do I adjust the priority of cache configuration?
Please see the directions in [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).

### I use my own server as the origin server of CDN. Can I configure it to not cache a specific type of files? Can I set the cache validity period to "0" to disable caching?
You can configure different cache validity periods for different types of directories and files. If the cache validity period is configured to 0, the CDN node will not cache the resource, in which case the CDN node needs to pull related resources from the origin server every time the users send access requests to the node. For more information on cache configurations, please see [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317).

### What cache validity configurations does Tencent Cloud support?
Tencent Cloud CDN supports cache validity configurations at various dimensions, custom priority adjustment, and cache inheritance policies (advanced cache validity configuration). A reasonable cache validity period can effectively improve the resource hit rate and lower origin-pull rate, reducing bandwidth usage.

### What is the default cache configuration of CDN?
The default configuration is as follows when a domain name is connected:
- External origin domain name connection: by default, the cache validity period for all files is 30 days, except for dynamic files (such as .php, .jsp, .asp, .aspx). The cache validity period for these dynamic files is 0 by default, which means any request for such files will be directly forwarded to the origin server.
- COS origin domain name connection: by default, the cache validity period for all files is 30 days.
- The advanced cache validity configuration is disabled by default.

### What are cache inheritance policies?
When a user makes a request for a certain business resource, the origin server's response HTTP header includes the `Cache-Control` field. The default policy is as follows:
- If the `Cache-Control` field is `max-age`, the cache validity period for this resource will be the period set for the resource, and will not inherit the value specified by `max-age`.
- If the `Cache-Control` field is `no-cache` or `no-store`, the CDN node will not cache the resource.

### What are cache matching rules?
When multiple caching policies are set, the priorities of the entries are determined on a bottom-to-top basis, with the entry at the bottom of list having the highest priority and the one at the top having the lowest priority. For example, suppose the following caching policies are set for a domain name:
```
All files (30 days)
.php .jsp .aspx 0 seconds
.jpg .png .gif 300 seconds
/test/*.jpg 400 seconds
/test/abc.jpg 200 seconds
```

If the domain name is `www.test.com`, and the resource is `www.test.com/test/abc.jpg`, the matching rule will be as follows:
1. Match with the first entry. It is hit, so the cache validity period is 30 days.
2. Match with the second entry. It is not hit.
3. Match with the third entry. It is hit, so the cache validity period is 300 seconds.
4. Match with the fourth entry. It is hit, so the cache validity period is 400 seconds.
5. Match with the fifth entry. It is hit, so the cache validity period is 200 seconds.

The final cache validity period is subject to the last matching result, and so it will be 200 seconds.
