## Overview
You can adjust the cache period of resources in browsers to optimize the browser cache and load requested resources more quickly.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/zh/contact-us) to get the permission.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Site Acceleration** > **Cache Configuration** on the left sidebar.
2. On the cache configuration page, select the target site and click **Set** in the browser cache TTL module.
![](https://qcloudimg.tencent-cloud.cn/raw/5d430dfdb036d8aa5c79604255e9a4e4.png)
3. In the browser cache TTL pop-up window, select a mode and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/12ffed7dc2306431d926d2c99c252933.png)

Parameter description:
 - Follow origin server (default configuration): The `Cache-Control` or `Last-Modified` header of the origin server will be followed.
 - No cache: Resources won't be cached in browsers.
 - Custom time: Customize the resource cache period.
   

Note: The overall cache policy is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/510dfa44965a955c325531746a1a625c.png)


