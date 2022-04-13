## Overview
After offline caching is enabled, when your origin server fails, and resources cannot be pulled through origin-pull normally, resources cached on nodes (even expired resources) can be used until the origin server recovers.
- If there is cached content on nodes, it will be returned. Even if the hit content has expired, it will still be returned until the origin server recovers to resume normal origin-pull.
- If there is no cached content on nodes, an error message indicating that the origin server fails will be returned.

>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Site acceleration** > **Cache configuration** on the left sidebar.
2. On the cache configuration page, select the target site and toggle offline caching on or off.
![](https://qcloudimg.tencent-cloud.cn/raw/66d3f8777404d04c753e618bac1d5a9c.png)

 - Enabled status (default): Offline caching is enabled.
 - Disabled status: Offline caching is disabled.

