CDN provides an Ignore Query String switch, which allows you to control whether to filter the parameters after **"?"** in user's request URL during caching. You can use this feature for flexible versioning or token-based authentication.
> If different parameters in your resource URL represent the same content, we recommend enabling the ignore query string feature to effectively improve the cache hit rate.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page.
2. Find the domain name you want to edit and click **Manage** in the operation column.
 ![](https://main.qcloudimg.com/raw/0ee1a8e25e86c513cfeaf1494bff81f1.jpg)
3. Click the **Access Control** tab and configure the ignore query string feature in the **Ignore Query String** module.
 ![](https://main.qcloudimg.com/raw/696b14c83d40fc433bef12f199dd8e5a.jpg)
> If your accelerated service type is download acceleration, video on-demand, or live video broadcasting, the ignore query string feature is enabled by default. If the service type is static acceleration, it is disabled by default.

## Sample Case
When CDN caches resources on the node storage structure, it looks up the stored resources based on the cache_key as an index.
1. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/e720e78f96e74ad7bfbde09b4de6a219.png)
 + User A requests a resource with URL `http://www.test.com/1.jpg?version=1.1`. When a node stores the resource, the corresponding `cache_key` is `www.test.com/1.jpg. ` with the parameters after "?" ignored.
 + User B requests a resource with URL `http://www.test.com/1.jpg?version=1.2`, which will also be looked up with `cache_key` as `www.test.com/1.jpg`. Therefore, the same content as requested by user A can be directly hit.
2. If the configuration is as follows:
 ![](https://main.qcloudimg.com/raw/696b14c83d40fc433bef12f199dd8e5a.jpg)
 + User A requests a resource with URL ```http://www.test.com/1.jpg?version=1.1```. When a node stores the resource, the corresponding ```cache_key``` is ```www.test.com/1.jpg?version=1.1``` with the parameters after "?" not ignored.
 - User B requests a resource with URL ```http://www.test.com/1.jpg?version=1.2```, which will be looked up with ```cache_key``` as ```www.test.com/1.jpg?version=1.2```. As there is no hit, the corresponding content will be obtained from the origin server for caching. 
