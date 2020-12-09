
## Configuration Overview

The resource cache in Tencent Cloud CDN is triggered by requests. When a user initiates an access request to a resource, if the CDN node receiving the request has not cached the requested resource, it will forward the request to the origin server to pull the resource. After the resource is successfully pulled by the node (with a 2XX status code returned), it will be cached on the node and returned to the user.

You cannot directly manage resources cached on CDN nodes. If you are worried that resources on the origin server will change but CDN nodes will still cache the legacy resources and return them to users, you can configure the node cache rules.


## Configuration Guide

### Viewing the Configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section.

When adding an acceleration domain name, default node cache validity rules are added based on different acceleration business types and can be modified as needed.
- If static acceleration is selected, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached by default, and other files will be set to follow the origin server by default.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- If downloading or streaming VOD acceleration is selected, the default cache time of all files will be 30 days.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adding Rules

Node cache validity rules support caching by specified file type, folder, and full-path file. You can add rules as needed.


- Follow origin server: follow the `Cache-Control` header of origin server.
- Cache: configure the cache time of resources on the node. It supports force cache, i.e., whether to ignore the `Cache-Control: no-store/no-cache/private` of the origin server.
- No cache: obtain resources from the origin server.

<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


#### Configuration limitations

- Each domain name can be configured with up to 20 cache rules.
- Rule priority can be adjusted: rules at the bottom of the list have higher priority.
**Note: the "All file - No max-age" rule has the lowest priority by default, and the priority cannot be adjusted.**
- In each rule of specified file type, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file type - jpg;png".
- If **Cache** is selected from the **Cache Option** and **Yes** is selected for **Force Cache**, CDN will cache according to the configured cache rules. If **No** is selected for **Force Cache** and the origin server is `Cache-Control: no-store/no-cache/private`, CDN will not cache resources to the nodes and will obtain resources from the origin server.

>! If there is any legacy node cache validity configuration (i.e., the basic mode), it will be upgraded comprehensively once it is submitted as the advanced mode and can no longer be restored to the basic mode.
### Modifying Rules

You can click **Modify** to modify the added cache rules.

### Deleting Rules

You can click **Delete** to delete the added cache rules.





## Configuration Samples

The node cache validity configurations for the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

The actual cache will be as follows:

- The node cache time for `www.test.com/abc.jpg` is 10 days.
- `www.test.com/def.php` will not be cached to the node.



