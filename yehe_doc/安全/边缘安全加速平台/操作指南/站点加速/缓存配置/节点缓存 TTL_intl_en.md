## Overview
You can adjust the cache period of resources on nodes to optimize the node cache, load requested resources more quickly, and remove old resources timely.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Site Acceleration** > **Cache Configuration** on the left sidebar.
2. On the cache configuration page, select a target site and click **Set** in the node cache TTL** module.
![](https://qcloudimg.tencent-cloud.cn/raw/9507c0e41ed6723a2aec1556713fd208.png)
3. In the node cache TTL pop-up window, select a behavior mode and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/907bcff297fbb7700001b9a159d83f9a.png)
    **Parameter description:**
    - Follow origin server (default configuration): The `Cache-Control` or `Last-Modified` header of the origin server will be followed.
    - No cache: Resources won't be cached on nodes.
    - Custom time: Customize the resource cache period.

Note: The overall cache policy is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/ff3e0f7407150bbf0c84c0c24eec02cf.png)

>? Force cache: It is enabled by default. When it’s enabled, node cache TTL will take effect within the cache period you configure, even if the origin server's `Cache-Control` is `no-cache/no-store/private`. When it’s disabled, the nodes will not cache resources and follow the no-cache header, even if the origin server's `Cache-Control` is `no-cache/no-store/private`. To disable force cache, you can go to [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151) to customize node cache TTL rules.
