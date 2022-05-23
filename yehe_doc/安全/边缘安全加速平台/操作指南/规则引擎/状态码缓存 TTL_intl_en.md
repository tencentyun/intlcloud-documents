
## Overview
Status code cache TTL specifies how long to cache origin response status codes on nodes, allowing the nodes to directly respond to non-2XX codes and reduce pressure on the origin server.

Currently supported status codes are as follows:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
>?The EdgeOne console is not yet fully available. To access the console, please [contact us](https://intl.cloud.tencent.com/contact-us) for activation.
>
2. On the rule engine page, select the target site and click ![img](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure status code cache TTL rules as needed.
3. On the rule engine page, select the operation **Status code cache TTL** and configure other parameters as needed. Click **Save and publish** or **Save only**.
>!Supported match types: "All (any request)", "Host", and "File extension".
>
