
## Configuration Scenario
Resource cache in Tencent Cloud CDN is triggered by requests. When a user initiates an access request to a resource, if the CDN node receiving the request has not cached the requested resource, it will forward the request to the origin server to pull the resource. After the resource is successfully pulled by the node (with a 2XX status code returned), it will be cached on the node and returned to the user.

You cannot directly manage resources cached on CDN nodes. If you are worried that resources on the origin server change but CDN nodes still cache the legacy resources and return them to users, you can configure node cache rules.

Each cached resource on CDN node has an expiration time. If the requested cached resource has expired, it will be considered as invalid even if the resource is still cached on the node. The node will pull the resource from the origin server again. Node cache rule allows you to configure the cache validity period for resources in a specific type, directory, and path. You can configure these items based on actual business scenarios.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Cache Configuration** tab, find the cache validity configuration.
When you connect an acceleration domain name:
+ If you select static acceleration, the default cache validity period of general dynamic files (such as .php, .jsp, .asp, and .aspx) will be 0 (direct origin-pull without caching), and the validity period for all other types of files will be 30 days.
+ If you select download acceleration or streaming VOD acceleration, the default cache validity period of all files will be 30 days.

![](https://main.qcloudimg.com/raw/43e457600f1d0036c23dff9d091da34d.png)

### Modifying configuration
#### 1. Modify the configuration
CDN currently allows you to configure cache validity rules in the following four formats:
+ File: cache validity period will be configured by the entered file extension. Different file extensions should be separated with `;`, such as `jpg;css`. 
+ Folder: cache validity period will be configured by the entered directory path in the format of `/test` and does not need to end with `/`. Different directories should be separated with `;`.
+ Full-path file: cache validity period will be configured by the entered full file path in the format of `/index.html`. The full file path and file type can be combined for match, such as `/test/*.jpg`.
+ Homepage: cache validity period will be configured for the root directory.

![](https://main.qcloudimg.com/raw/b9be3726c932508d5705a773816cea26.png)
**Configuration rules:**

+ You can configure up to 10 cache validity rules.
+ If there are multiple cache validity rules, the one at the bottom has the highest priority.
+ You can configure the validity period to up to 365 days.

> !If your acceleration domain name is configured for global acceleration, the configured cache validity period will take effect globally. This configuration does not distinguish between requests from and outside of the Chinese mainland.

#### 2. Platform policies
When a user makes a request for a certain business resource and the origin server's HTTP response header includes the `Cache-Control` field, the default policy will be as follows:
- If the `Cache-Control` field is `Max-Age`, the cache validity period for this resource is subject to that configured for the node, rather than the value specified by `Max-Age`.
- If the `Cache-Control` field is `no-cache`, `no-store`, or `private`, the CDN node will not cache the resource.
- If the `Cache-Control` field does not exist, when the request hits the CDN cache, CDN will add the "Cache-Control:max-age = 600" header by default. 

#### 3. Advanced cache configuration
After advanced cache configuration is enabled, you can adjust the node cache validity period dynamically by configuring the `Max-Age` value in the HTTP response header `Cache-Control` of the origin server.

After advanced cache configuration is enabled, CDN will compare the configured node cache validity period with the `Max-Age` value and take the smaller one as the actual validity period.
+ If `Max-Age` configured for `/index.html` of the origin server is 200 seconds and the cache validity period configured for CDN is 600 seconds, the actual cache validity period of the file will be 200 seconds.
+ If `Max-Age` configured for `/index.html` of the origin server is 800 seconds and the cache validity period configured for CDN is 600 seconds, the actual cache validity period of the file will be 600 seconds.

> !After advanced cache configuration is enabled, if the origin server does not return the `Last-Modified` field, CDN will add it by default and change its value once every 10 minutes.

## Configuration Sample
Suppose the cache validity rule configured for the acceleration domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/36a6bfe2001e73c0a8a24e669c1b3a52.png)
The actual cache validity period will be as follows:

1. 200 seconds for the `/test/abc.jpg` file.
2. 400 seconds for the `/test/def.jpg` file.
3. 300 seconds for the `/test/1.png` file.

