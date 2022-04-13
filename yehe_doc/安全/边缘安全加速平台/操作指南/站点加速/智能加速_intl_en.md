As a premium service provided by EdgeOne, smart acceleration uses route optimization to process your business access requests more quickly, stably, and securely. EdgeOne intelligently selects the optimal transfer route based on the real-time network latency to minimize problems between your server and end users, such as high network latency, connection errors, and request failures.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Overview

#### Dynamic resources
Smart acceleration can be used in scenarios where dynamic content needs to be requested frequently, including online game, ecommerce, finance, payment, and online education.

#### Dynamic and static resources
For dynamic content use cases, you can refer to the above scenarios. Your static content still provides service through data cached on edge servers. In addition, when any cached content expires, it will be quickly updated through smart acceleration.

## Directions
To enable smart acceleration for all domains added in EdgeOne, set the proxy mode of the corresponding subsites to **Secure acceleration** on the DNS service page.

>? If you enable **smart acceleration** for your site in the smart acceleration configuration or enable smart acceleration for the corresponding **subdomain** in the rule engine, secure acceleration will be enabled for the selected site or subdomain, and additional fees will be incurred.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **DNS service** on the left sidebar.
2. On the DNS service page, select the target site and click **Record management**.
3. On the record management page, select the target record, click **Edit**, change the proxy mode to **Secure acceleration**, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/95410cf671fe524e0264bf036cb1505e.png)

## Notes
- To enable smart acceleration for you domain, you need to add the corresponding record on the **DNS service** page in the EdgeOne console and switch to the secure acceleration mode.
- As smart acceleration is a value-added service provided by EdgeOne, additional usage fees will be incurred. Before enabling this feature, read the billing description on the **Secure acceleration page**.
>? For more billing details, contact us, and we will evaluate the prices based on your business conditions.
