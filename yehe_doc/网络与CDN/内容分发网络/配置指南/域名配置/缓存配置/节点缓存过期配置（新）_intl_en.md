## Configuration

Object caching is triggered by requests. When a CDN node receives a request, and the cache of the requested object is not available, the request will be forwarded to the origin. Then the object is pulled and cached on the CDN node, and served to the requester.

You cannot directly manage resources cached on CDN nodes. However you can control caching by setting up node caching policies, for example, to ensure that the served resource is fresh.

>! Currently, a file up to 32 GB can be cached. Objects over 32 GB will be served from the origin.

## Directions

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** in the left sidebar, locate the desired domain name, and click **Manage** -> **Cache Configuration** -> **Node Cache Validity Configuration**.

When you add a domain name, a node cache validity rule is added by default according to the acceleration type. You can change it if needed.

- **Static acceleration**:  common dynamic files (such as PHP, JSP, ASP, and ASPX files) are not cached by default, and cache of other files will be valid for 30 days by default.
 ![](https://main.qcloudimg.com/raw/5f48bc5246397975544baadf5ac81f4e.png)
- For download or on-demand video streaming acceleration, the default cache validity of all files will be 30 days.
![](https://main.qcloudimg.com/raw/cdd00154330b8cb217287874f4f40693.png)

### Adding rules

Node cache rules can be applied to specified file extension (such as `jpg;png`), folders (such as `/test`), and full-path files (such as `/test/1.jpg`):
<img src="https://main.qcloudimg.com/raw/5454a77683dca1cfb491eccdae839aa4.png" height="207" width="408" />

- Follow origin server: follow the `Cache-Control` header of the origin server.
- When the HTTP response header of the origin server contains the field `Cache-Control`:
  If `Cache-Control` is `max-age`, the max-age value will be used as the node cache validity.
   If `Cache-Control` is `no-cache/no-store/private`, then the CDN node will not cache the resource.
- If the HTTP response header of the origin server does not contain the field `Cache-Control`, then the CDN node will not cache the resource.
  **Note:** some platforms may have the default policy: When a resource is requested for the first time, the request will be forwarded to the origin server and CDN nodes will cache the resource. If the resource is requested again and the node is hit, CDN will add the response header `Cache-Control: max-age=600`.
- **Cache**: configure the resource cache validity on nodes.
- **Force cache**: configure whether to ignore the `Cache-Control: no-cache/no-store/private` of the origin server. It defaults to "No".
  **Note:** If **Force cache** is configured as **Yes**, node cache validity will be set to the value configured here.
  　　If **Force cache** is configured as **No** and the `Cache-Control` field of the origin server is `no-cache/no-store/private`, then CDN nodes will not cache resources even the cache validity is configured.
- No cache: CDN nodes do not cache resources.





#### Configuration limitations

- A maximum of 100 caching rules can be added for a single domain name.
- You can re-arrange the rules to adjust their priorities. Rules at lower places have higher priorities.
  **Note:** The **No max-age** feature is being upgraded and currently not supported. Please stay tuned for the official launch. If you have configured the rule, please delete it or modify the rule to **All Files**.
- In each rule of specified file extension, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file extension - jpg;png".

>! If there is any legacy node cache validity configuration (i.e., the basic mode), it will be upgraded comprehensively once it is submitted as the advanced mode and can no longer be restored to the basic mode.



### Default policies

If no rule is configured or matches requests, the default policies will be applied:

- When a user makes a request for a certain business resource, if the HTTP response header of the origin server contains the field `Cache-Control`, the `Cache-Control` will be followed.
- If the HTTP response header of the origin server does not contain the field `Cache-Control`, then the resource cache validity on nodes will be 600 seconds.

## Configuration Samples

If the node cache validity configurations for the acceleration domain name `www.test.com` are as follows:
![](https://main.qcloudimg.com/raw/c1402003c4549d2e6035420921f67bd0.png)

The actual cache will be as follows:

- Even though `Cache-Control` is `no-cache/no-store/private`, the validity of `www.test.com/abc.jpg` is 10 days.
- `www.test.com/def.php` will not be cached to nodes.
