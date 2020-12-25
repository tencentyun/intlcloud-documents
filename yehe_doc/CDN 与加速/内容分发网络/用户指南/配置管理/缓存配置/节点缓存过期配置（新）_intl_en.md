
## Configuration Overview

The resource cache in Tencent Cloud CDN is triggered by requests. When a user initiates an access request to a resource, if the CDN node receiving the request has not cached the requested resource, it will forward the request to the origin server to pull the resource. After the resource is successfully pulled by the node (with a 2XX status code returned), it will be cached on the node and returned to the user.

You cannot directly manage resources cached on CDN nodes. If you are worried that resources on the origin server will change but CDN nodes will still cache the legacy resources and return them to users, you can configure the node cache rules.


## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section.

When adding an acceleration domain name, default node cache validity rules are added based on different acceleration business types and can be modified as needed.
- If static acceleration is selected, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached by default, and other files will be set to follow the origin server by default.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- If download or streaming VOD acceleration is selected, the default cache validity of all files will be 30 days.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adding rules

Node cache validity rules support caching by specified file type, folder, and full-path file.
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


- Follow origin server: follow the `Cache-Control` header of origin server.
 - When the `Cache-Control` field exists in the corresponding HTTP response header of the origin server, then:
 If the `Cache-Control` field is `max-age`, the CDN node cache validity will be the `max-age` value.
 If the `Cache-Control` field is `no-cache`, `no-store`, or `private`, the CDN node will not cache resources.
 - If the `Cache-Control` field does not exist in the corresponding HTTP response header of the origin server, the CDN node will not cache resources.
**Note: **Some platforms may have the following default policy: CDN nodes forward the first request to the origin server and cache the requested resources. If the same resources are requested again and the cache is hit, CDN will add the header `Cache-Control: max-age=600` by default.
- Cache: configure the validity of resources on the node.
- Force cache: if **Cache** is selected as the cache option, you can choose whether to perform force cache, i.e., whether to ignore the `Cache-Control: no-cache/no-store/private` of the origin server (**No** is ticked by default).
**Note**: If **Yes** is ticked, the CDN node cache validity will be the value configured here.
　　If **No** is ticked and the `Cache-Control` field of the origin server is `no-cache`, `no-store`, or `private`, CDN nodes will not cache resources even though the cache validity is configured.
- No cache: CDN nodes do not cache resources.




#### Configuration limitations

- Each domain name can be configured with up to 20 cache rules.
- Rule priority can be adjusted: rules at the bottom of the list have higher priority.
**Note**: the "Type: All files; Content: No max-age" rule has the lowest priority by default, and the priority cannot be adjusted.
- In each rule of specified file type, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file type: jpg;png".


>! If there is any legacy node cache validity configuration (i.e., the basic mode), it will be upgraded comprehensively once it is submitted as the advanced mode and can no longer be restored to the basic mode.





## Configuration Samples

The node cache validity configurations for the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

The actual cache will be as follows:

- The node validity for `www.test.com/abc.jpg` is 10 days, even though the `Cache-Control` field of the origin server is `no-cache`, `no-store`, or `private`.
- `www.test.com/def.php` will not be cached to the node.



