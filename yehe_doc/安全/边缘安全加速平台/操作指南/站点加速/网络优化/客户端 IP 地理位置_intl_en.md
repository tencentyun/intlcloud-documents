## Overview
The custom header can carry the geographical location information of the client IP to the origin.
>?
>- The country/region value is represented by an ISO 3166-1 alpha-2 code (a two-letter country/region code).
>- Currently, IPv6 is not supported.
>
## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Site Acceleration** > **Network optimization** on the left sidebar.
2. On the **Network optimization** page, select the target site and click ![img](https://qcloudimg.tencent-cloud.cn/raw/8d3e9bac718473e40a340843b4cc7fb8.png) to enable **Client IP Geographical Location**.
3. In the pop-up window, customize the header name or directly use the default name `EO-Client-IPCountry` and click **Save**.
>?The configuration on this page is global, that is, it takes effect for all requests of the current site. If a subdomain name or request path requires custom configuration, click [Rule Engine](https://intl.cloud.tencent.com/document/product/1145/46151) on the left sidebar to create custom configuration at a fine granularity.

