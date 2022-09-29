## Overview
Range GETs can be enabled to reduce the consumption of large file origin-pulls and response time.

#### Why can Range GETs improve the efficiency of large file delivery?

When caching large files, nodes will split them into smaller parts in order to improve cache efficiency. All parts cached expire at the same time and follow the node cache TTL configuration. Range requests are also supported. For example, if a client request carries the HTTP header `Range: bytes = 0-999`, only the first 1000 bytes of the file will be returned to the user.

If Range GETs is enabled: When parts of the file are requested and their caches expire, nodes only pull and cache the requested parts and return them to the user, so that origin-pull consumption and response time are greatly reduced.

If Range GETs is disabled, when the client requests only parts of a file, the node will pull only the requested parts according to the `Range` header in the client request, cache them, and return them to the client at the same time. However, this may not be able to achieve the optimal performance. In large file scenarios, we recommend you enable Range GETs.

## Use Cases
You can use Range GETs to cache large static files in either of the following cases: The origin server supports Range requests, or you use a Tencent Cloud COS origin server and do not apply any data processing methods such as image processing.

## Notes
- The origin server must support Range requests, or the origin-pull may fail.
- The origin-pull may fail if Range GETs is enabled for small static files, or if you enable it while using a Tencent Cloud COS origin server and data processing methods such as image processing.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![img](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure Range GETs rules as needed.
3. On the rule engine page, select the operation **Range GETs** and configure other parameters as needed. Click **Save and publish** or **Save only**.
>! Currently, supported match types include host, URL path, and file extension.

   
