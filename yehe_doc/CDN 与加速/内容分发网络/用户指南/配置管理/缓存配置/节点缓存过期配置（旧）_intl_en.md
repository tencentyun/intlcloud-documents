The node cache validity configuration is updated with an advanced mode, supporting more refined configurations. For more information, please see [Node Cache Validity Configuration (New)](https://intl.cloud.tencent.com/document/product/228/38424). 

## Configuration Overview
The resource cache in Tencent Cloud CDN is triggered by requests. When a user initiates an access request to a resource, if the CDN node receiving the request has not cached the requested resource, it will forward the request to the origin server to pull the resource. After the resource is successfully pulled by the node (with a 2XX status code returned), it will be cached on the node and returned to the user.

You cannot directly manage resources cached on CDN nodes. If you are worried that resources on the origin server will change but CDN nodes will still cache the legacy resources and return them to users, you can configure the node cache rules.

Each cached resource on a CDN node has an expiration time. If the requested cached resource has expired, it will be considered invalid even if the resource is still cached on the node. The node will pull the resource from the origin server again. The node cache rule allows you to configure the cache validity period for resources in a specific type, directory, and path. You can configure these items based on your actual business scenarios.

## Configuration Guide
### Viewing the Configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section.
![](https://main.qcloudimg.com/raw/834d620b98c9d7d387547e59a7e6a1f4.png)

### Adding Rules

CDN currently supports configuring node cache validity rules in the following four types:
+ File: the cache validity period can be configured by the entered file extension. Different file extensions should be separated with `;`, i.e., `jpg;css`.
+ Folder: the cache validity period can be configured by the entered directory path in the format of `/test` and does not need to end with `/`. Different directories should be separated with `;`.
+ Full-path file: the cache validity period can be configured by the entered full file path in the format of `/index.html`. The full file path and file type can be combined for matching, such as `/test/*.jpg`.
+ Homepage: the cache validity period can be configured by the root directory.

![](https://main.qcloudimg.com/raw/1a72478ce0bc4fc1ef6a22bcb8064a6b.png)
**Configuration limitations**

- Each domain name can be configured with up to 20 cache rules.
- Rule priority can be adjusted: rules at the bottom of the list have higher priority.
- In each rule of specified file type, folder, and full-path file, up to 100 groups of contents can be entered. Please use ";" to separate different contents, e.g., "Specified file type - jpg;png".
- The cache time can be set as up to 365 days.

#### Default policy
When a user makes a request for a certain business resource and the origin server's HTTP response header includes the `Cache-Control` field, the default policy will be as follows:
- If the `Cache-Control` field is `Max-Age`, the cache validity period for this resource is subject to that configured for the node, rather than the value specified by `Max-Age`.
- If the `Cache-Control` field is `no-cache`, `no-store`, or `private`, then the CDN node will not cache the resource.


#### Advanced cache validity configuration switch
After it is enabled, CDN will compare the cache time of the matched cache rule with the origin server's "max-age" value, and then adopt the smaller value as the cache time.

- If the `Max-Age` configured for `/index.html` of the origin server is 200 seconds, and the cache time configured for CDN is 600 seconds, then the actual cache time of the file will be 200 seconds.
- If the `Max-Age` configured for `/index.html` of the origin server is 800 seconds, and the cache time configured for CDN is 600 seconds, then the actual cache time of the file will be 600 seconds.

>! After it is enabled, if the origin server does not return the `Last-Modified` field, CDN will add it by default and change its value once every 10 minutes.

#### Follow origin server switch
After it is enabled, if a request does not match any cache rules, the origin server will be followed.

>! The follow origin server switch and the advanced cache validity configuration switch cannot be enabled at the same time.


## Configuration Samples
The node cache validity configurations for the acceleration domain name `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/a585a6b560cb0e555b71e08bea179353.png)
The actual cache time will be as follows:
1. 400 seconds for the `/test/def.jpg` file.
2. 5 minutes for the `/test/1.png` file.
3. 30 days for other files.
