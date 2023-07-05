> Cache validity period configuration refers to a set of expiration rules that CDN cache nodes follow when caching your business content. All resources cached on CDN nodes have an expiration time. For unexpired resources, when a request reaches the node, the node will directly return the requested resource to the user to speed up resource delivery. For expired resources, the node will forward the user request to the origin server, get the resource again, cache and return it to the user.
>
> Tencent Cloud CDN supports custom priority adjustment and content cache validity period configuration at various dimensions. A proper cache validity period can effectively improve the hit rate and lower the origin-pull rate, helping reduce bandwidth usage.
>
> Tencent Cloud CDN supports cache validity period configuration based on 403 and 404 status codes.

## Browser cache validity period configuration

### Configuration guide

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click "Manage" on the right of the domain name to be edited.
![](https://main.qcloudimg.com/raw/6929c1aad9f35dc962ee9bb6b1883fd1.png)
Click **Cache Configuration** and you can see the **Browser Cache Validity Configuration** module:
![](https://main.qcloudimg.com/raw/bc4443809045e0fd41aea9de9aad6a91.png)

When a domain name is being connected to CDN, no browser cache validity period configuration will be set by default.

### Modifying configuration

Click **New Cache Expiration Rule**. You can add browser cache validity configuration based on business needs. CDN supports 4 ways of configuring the browser cache validity period:

#### 1. Configure a cache validity period for all files

You can configure a cache validity period for all files as shown below (content is always ```all``` and cannot be modified):
![](https://main.qcloudimg.com/raw/0f95aac2450e40f983c489c0abb97ff9.png)

If purge time is configured as 0, the content will not be cached. The maximum cache validity period is 365 days.

#### 2. Configure a cache validity period by file type

You can enter a file extension to configure a cache validity period by file type, as shown below:
![](https://main.qcloudimg.com/raw/f39b3489c1e630e89be446ea620bbc76.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and must be a file extension beginning with `` `.```, such as ` ``.png` ``. If purge time is configured as 0, the content will not be cached. The maximum cache validity period is 365 days.

#### 3. Configure a cache validity period by folder
You can enter the folder path to configure a cache validity period by folder, as shown below:
![](https://main.qcloudimg.com/raw/446a2c3b97e6a44c46e04f8e23a8861a.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and must be a folder beginning with ```/ ```. If purge time is configured as 0, the content will not be cached. The maximum cache validity period is 365 days.

#### 4. Configure a cache validity period by full file path
You can configure a cache validity period for a specified file as shown below:
![](https://main.qcloudimg.com/raw/a8a4daf2f05b2b8aa368043fd32a10be.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and file type matching by ```*``` is supported, such as ```/test/abc/*.jpg```:

![](https://main.qcloudimg.com/raw/164dccad7d838f13ba63e033db7cc056.png)

### Priority
If multiple cache policies are configured, their priorities are determined on a bottom-to-top basis, with the one at the bottom of the list having the highest priority and the one at the top having the lowest priority. For example, if the following cache policies are configured for a domain name:
> All files: 30 days
> .php, .jsp, .aspx: 0 seconds
> .jpg, .png, .gif: 300 seconds
> /test/*.jpg: 400 seconds
> /test/abc.jpg: 200 seconds

If the domain is ```www.test.com``` and the resource is ```www.test.com/test/abc.jpg```, then the matching rule is as follows:
1. Match with the first policy. It is hit, so the cache validity period will be 30 days.
2. Match with the second policy. It is missed.
3. Match with the third policy. It is hit, so the cache validity period will be 300 seconds.
4. Match with the fourth policy. It is hit, so the cache validity period will be 400 seconds.
5. Match with the fifth policy. It is hit, so the cache validity period will be 200 seconds.

The actual cache validity period is subject to the last matching result and will be 200 seconds.

Click **Adjust priority** to adjust the priorities of cache validity period configurations as needed.
![](https://main.qcloudimg.com/raw/171626f31f5319307a686542cdde724d.png)
Use the up and down arrows on the right to adjust the priorities of cache validity period configurations and click **Save** to complete the adjustment.
![](https://main.qcloudimg.com/raw/2624ef89c57ec87b881844c7c3e5e985.png)
## Node cache validity period configuration

### Configuration guide

Below the **Browser Cache Validity Configuration** module, you can see the **Node Cache Validity Configuration** module:
![](https://main.qcloudimg.com/raw/d2bb31c0cd42af7c3595876c69da1538.png)

When a domain name is being connected to CDN, the node cache validity period configuration is not set by default. You can add it manually.

The node cache validity period configuration follows the `max-age` header of the packet returned by the origin server by default:

1. If no CDN node cache rule is configured or the cache rule configured for the node is not hit by a request, CDN node cache validity period will be subject to the `max-age` header from the origin server;
2. If there is no `max-age` header in the packet returned by the origin server, CDN node will not cache the corresponding type of files by default.

### Modifying configuration

Click **New Cache Expiration Rule**. You can add node cache validity period configuration based on business needs. CDN supports 5 ways of configuring node cache validity period:

#### 1. Configure a cache validity period for files without `max-age` header

When a resource is requested, if there is no `max-age` header in the packet returned by the origin server, you can choose to configure a cache validity period for files without `max-age` header, as shown below (content is always `Without max-age` and cannot be modified):
![](https://main.qcloudimg.com/raw/8999430249579e54a8a06fc5c68c1624.png)

If purge time is configured as 0, the content will not be cached and all requests will be forwarded to the origin server. The maximum cache validity period is 365 days.	

#### 2. Configure a cache validity period for all files

You can configure a cache validity period for all files as shown below (content is always ```all``` and cannot be modified).

If purge time is configured as 0, the content will not be cached and all requests will be forwarded to the origin server. The maximum cache validity period is 365 days.

#### 3. Configure a cache validity period by file type

You can enter a file extension to configure a cache validity period by file type, as shown below:
![](https://main.qcloudimg.com/raw/0304515d54631190676fa89d741baefd.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and must be a file extension beginning with `` `.```, such as ` ``.png` ``. If purge time is configured as 0, the content will not be cached and all requests will be forwarded to the origin server. The maximum cache validity period is 365 days.

#### 4. Configure a cache validity period by folder

You can enter the folder path to configure a cache validity period by folder, as shown below:
![](https://main.qcloudimg.com/raw/7348c4fd5bac84ab3ac2da8243f37e06.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and must be a folder beginning with ```/ ```. If purge time is configured as 0, the content will not be cached and all requests will be forwarded to the origin server. The maximum cache validity period is 365 days.

#### 5. Configure a cache validity period by full file path

You can configure a cache validity period for a specified file as shown below:
![](https://main.qcloudimg.com/raw/f261692ed87757a63b9e5a44fa2d304c.png)

Multiple items can be entered, which should be separated by `` `;` ``. The entry is case-sensitive and file type matching by ```*``` is supported, such as ```/test/abc/*.jpg```:

![](https://main.qcloudimg.com/raw/e71cb7093da2dc15ae055574a69c5088.png)

### Priority

If multiple cache policies are configured, their priorities are determined on a bottom-to-top basis, with the one at the bottom of the list having the highest priority and the one at the top having the lowest priority. For example, if the following cache policies are configured for a domain name:

> All files: 30 days
> Without `max-age`: 60 seconds
> .php, .jsp, .aspx: 0 seconds
> .jpg, .png, .gif: 300 seconds
> /test/*.jpg: 400 seconds
> /test/abc.jpg: 200 seconds

If the domain is ```www.test.com```, the resource is ```www.test.com/test/abc.jpg```, and the header of the packet returned by the origin server is ```Cache-Control: max-age=600```, then the matching rule is as follows:

1. Match with the first policy. It is hit, so the cache validity period will be 30 days.
2. Match with the second policy. It is missed.
3. Match with the third policy. It is missed.
4. Match with the fourth policy. It is hit, so the cache validity period will be 300 seconds.
5. Match with the fifth policy. It is hit, so the cache validity period will be 400 seconds.
6. Match with the sixth policy. It is hit, so the cache validity period will be 200 seconds.

The actual cache validity period is subject to the last matching result and will be 200 seconds.

Click **Adjust priority** to adjust the priorities of cache validity period configurations as needed.
![](https://main.qcloudimg.com/raw/e29f4626385657d9788488a7c25ff95d.png)
Use the up and down arrows on the right to adjust the priorities of cache validity period configurations and click **Save** to complete the adjustment.
![](https://main.qcloudimg.com/raw/6c44f0872e9b06a6e5a7b1f7ccb12629.png)

## Header Cache

When a resource is hit in the node cache, CDN will cache the following headers from the origin server and return them to the user by default:

+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges 



## Status Code Cache

When a CDN node requests a resource from the origin server, in addition to the above cache policies, it will also cache the resource according to the cache configurations you set for 403 and 404 status codes:

You can adjust the 403/404 cache validity period in the **Status code cache** module under **Cache Configuration**: ![](https://main.qcloudimg.com/raw/ff0f8886ae228d3d212d9d3d7233fb26.png)

The cache validity period for 403/404 status code can be between 0 and 365 days.

**Note**: if the cache validity period of a file is 0 and a 403/404 status code is generated, it will still follow the no-cache policy for direct passthrough.
