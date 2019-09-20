CDN provides an Ignore Query String switch, which allows you to control whether to filter the parameters after **"?"** in user's request URL during caching. You can use this feature for flexible versioning or token-based authentication.
> If different parameters in your resource URL represent the same content, it is recommended to enable the ignore query string feature to effectively improve the cache hit rate.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the row of the domain name to be edited and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/18a3dd6931e3fe4ea109f971e5afe410.png)
3. Click the **Access Control** tab and configure the ignore query string feature in the **Ignore Query String** module.
 ![](https://main.qcloudimg.com/raw/77b13228a87729324cb0c27f6b17af3e.png)
> If your accelerated business type is download, video on-demand, or live video broadcasting, the ignore query string feature is enabled by default. If the type is static content, it is disabled by default.

## Configuration Case
When CDN caches resources on the node storage structure, it looks up the stored resources based on the cache_key as an index.
1. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/989e3e911163345f523ac6567f134289.png)
 + User A requests a resource with URL `http://www.test.com/1.jpg?version=1.1`. When a node stores the resource, the corresponding `cache_key` is `www.test.com/1.jpg. ` with the parameters after "?" ignored.
 + User B requests a resource with URL `http://www.test.com/1.jpg?version=1.2`, which will also be looked up with `cache_key` as `www.test.com/1.jpg`. Therefore, the same content as requested by user A can be directly hit.
2. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/cb67d1acee6ff68f06e7c33b2016d78c.png)
 + User A requests a resource with URL ```http://www.test.com/1.jpg?version=1.1```. When a node stores the resource, the corresponding ```cache_key``` is ```www.test.com/1.jpg?version=1.1``` with the parameters after "?" not ignored.
 - User B requests a resource with URL ```http://www.test.com/1.jpg?version=1.2```, which will be looked up with ```cache_key``` as ```www.test.com/1.jpg?version=1.2```. As there is no hit, the corresponding content will be obtained from the origin server for caching. 
