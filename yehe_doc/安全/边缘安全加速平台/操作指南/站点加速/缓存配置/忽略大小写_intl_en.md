## Overview
You can choose to or not to ignore the letter case of client request URLs as needed to optimize the node cache and load requested resources more quickly.

#### How does the letter case affect node cache?
When a node responds to a resource request, it will use the complete request URL as the cache key to match the cached resource and follow the letter case of the original request URL. Even if URLs in different letter cases have the same content, they will match different node caches. For example, `https://www.example.com/images/demo.JPG` and `https://www.example.com/images/demo.jpg` will be identified as different resource requests. If the resource is not on the node, the request will be forwarded for origin-pull, which increases the origin-pull traffic.

If `demo.jpg` does not vary by letter case (that is, even if in different letter cases, `demo.jpg` indicates the same image), then you can ignore the letter case to unify the requests to match the same node cache. For example, both `https://www.example.com/images/demo.jpg` and `https://www.example.com/images/demo.JPG` match the cached resource `https://www.example.com/images/demo.jpg`.

Check the impact of the letter case on resources in business resource URLs and use the **case ignoring** feature to optimize the cache accordingly.

>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
2. On the cache configuration page, select the target site and toggle case ignoring on or off.
![](https://qcloudimg.tencent-cloud.cn/raw/f406c89142b64678315ed6ad0b485704.png)

**Parameter description:**
 - Disabled status (default configuration): Request URLs are case-sensitive. Even if URLs in different letter cases have the same content, they will still be considered different resources.
 - Enabled status: Request URLs are case-insensitive. URLs with the same content but in different letter cases will be considered the same resource.


## Notes
This feature doesn't affect origin-pull request URLs and only changes the cache key of request on nodes. The origin-pull request URLs are the same as the URLs of original requests initiated by clients.



