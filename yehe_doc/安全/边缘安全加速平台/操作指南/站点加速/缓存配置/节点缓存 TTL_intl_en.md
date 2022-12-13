## Overview
You can adjust the cache period of resources on nodes to optimize the node cache, load requested resources more quickly, and remove old resources timely.

>?
>- EdgeOne will determine whether a resource cached on a node expires based on the cache validity period configured in **EdgeOne Node Cache TTL**.
>- If the cache of a resource accessed by a client doesn't expire on the node, the node will directly return the cached resource to the client.
>- If a resource accessed by a client is not cached, or the resource cache has expired on the node, the node will pull the latest resource from the origin server to cache it and return it to the client.
>- After a resource on the origin server is updated, its cache on the node needs to be updated immediately. You can use the [cache purge](https://intl.cloud.tencent.com/document/product/1145/46179) feature to clear historical caches that haven't expired on the node, so that the latest resources can be requested from the origin server.



## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site Acceleration** > **Cache configuration** on the left sidebar.
2. On the **Cache configuration** page, select the target site and click **Set** in the **EdgeOne Node Cache TTL** module.
![](https://qcloudimg.tencent-cloud.cn/raw/9507c0e41ed6723a2aec1556713fd208.png)
3. In the pop-up window, select a behavior and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/907bcff297fbb7700001b9a159d83f9a.png)
  **Parameter description:**
    - Follow origin server (default configuration): The `Cache-Control` header of the origin server will be followed. If the origin server has no CC headers, there will be no cache. You can also set a default cache time for overwriting.
    - No cache: Resources won't be cached on nodes.
    - Custom time: Customize the resource cache period.

Note: The overall cache policy is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ff3e0f7407150bbf0c84c0c24eec02cf.png)
>? Force cache: It is enabled by default. When it's enabled, node cache TTL will take effect within the cache period you configure, even if the origin server's `Cache-Control` is `no-cache/no-store/private`. When it's disabled, the nodes will not cache resources and follow the no-cache header, even if the origin server's `Cache-Control` is `no-cache/no-store/private`. To disable force cache, you can go to [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151) to customize node cache TTL rules.
