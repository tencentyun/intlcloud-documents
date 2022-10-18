## Overview
Host header rewriting enables you to rewrite the host header to the actual origin domain when the origin domain is different from the acceleration domain in the [load balancing](https://intl.cloud.tencent.com/document/product/1145/46193) task.

## Directions

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Origin Configuration** >**Rule Engine** on the left sidebar.
2. On the rule engine page, select the target site and click ![img](https://qcloudimg.tencent-cloud.cn/raw/fe4d4900f8ad69d506adc49bdb70fa32.png) to configure host header rules as needed.
3. On the rule engine page, select **Host** for the match type and **Rewrite host header** for the action, and configure other parameters as needed. Click **Save and publish** or **Save only**.
>? Supported match types: "Host".
