
## Configuration Overview

The resource cache in Tencent Cloud CDN is triggered by requests. When a user initiates an access request to a resource, if the CDN node receiving the request has not cached the requested resource, it will forward the request to the origin server to pull the resource. After the resource is successfully pulled by the node (with a 2XX status code returned), it will be cached on the node and returned to the user.

You cannot directly manage resources cached on CDN nodes. If you are worried that resources on the origin server will change but CDN nodes will still cache the legacy resources and return them to users, you can configure the node cache rules.


## Configuration Guide

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section.

When adding an acceleration domain name, default node cache validity rules are added based on different acceleration service types and can be modified as needed.
- If static acceleration is selected, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached by default, and other files will be set to follow the origin server by default.
![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- If download or streaming VOD acceleration is selected, the default cache validity of all files will be 30 days.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adding rules

Node cache rules can be applied to specified file types, folders, and full-path files:
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />


- Follow origin server: follow the `Cache-Control` header of the origin server.
 - When the HTTP response header of the origin server contains the field `Cache-Control`:
 If `Cache-Control` is `max-age`, the max-age value will be used as the node cache validity.
 If `Cache-Control` is `no-cache/no-store/private`, then the CDN node will not cache the resource.
 - If the HTTP response header of the origin server does not contain the field `Cache-Control`, then the CDN node will not cache the resource.
**Note:** Some platforms may have the default policy: When a resource is requested for the first time, the request will be forwarded to the origin server and CDN nodes will cache the resource. If the resource is requested again and the node is hit, CDN will add the response header `Cache-Control: max-age=600`.
- Cache: configure the resource cache validity on nodes.
- Force cache: configure whether to ignore the `Cache-Control: no-cache/no-store/private` of the origin server. It defaults to "No".
**Note:** If force cache is configured as "Yes", node cache validity will be set to the value configured here.
　　If force cache is configured as "No" and the `Cache-Control` field of the origin server is `no-cache/no-store/private`, then CDN nodes will not cache resources even the cache validity is configured.
- No cache: CDN nodes do not cache resources.






#### Configuration limitations

- A maximum of 20 caching rules can be added for a single domain name.
- Rule priority can be adjusted: rules at the bottom of the list have higher priority.
**Note:** The "No max-age" feature is being upgraded and currently not supported. Please stay tuned for the official launch. If you have configured the rule, please delete it or modify the rule to "All Files".
- In each rule of specified file type, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file type - jpg;png".


>! If there is any legacy node cache validity configuration (i.e., the basic mode), it will be upgraded comprehensively once it is submitted as the advanced mode and can no longer be restored to the basic mode.



### Default policies

The default policies below will be applied if there is no rule configured or hit.
- When a user makes a request for a certain business resource, if the HTTP response header of the origin server contains the field `Cache-Control`, the `Cache-Control` will be followed.
- If the HTTP response header of the origin server does not contain the field `Cache-Control`, then the resource cache validity on nodes will be 600 seconds.

## Configuration Samples

The node cache validity configurations for the acceleration domain name `www.test.com` is as follows:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

The actual cache will be as follows:

- Even though `Cache-Control` is `no-cache/no-store/private`, the validity of `www.test.com/abc.jpg` is 10 days.
- `www.test.com/def.php` will not be cached to nodes.



