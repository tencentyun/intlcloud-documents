## Overview
You can adjust the cache period of resources on nodes to optimize the node cache, load requested resources more quickly, and remove old resources timely.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
2. On the cache configuration page, select the target site and click **Settings** in the node cache TTL module.
![](https://qcloudimg.tencent-cloud.cn/raw/9507c0e41ed6723a2aec1556713fd208.png)
3. In the node cache TTL pop-up window, select a behavior mode and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/907bcff297fbb7700001b9a159d83f9a.png)
   
   **Parameter description:**
   
    - Follow origin server (default configuration): The `Cache-Control` or `Last-Modified` header of the origin server will be followed.
    - Do not cache: Resources won't be cached on nodes.
    - Custom time: Customize the resource cache period.

Note: The overall cache policy is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fd4fca0c7d137e7d97e8e56edda6a3c2.png)