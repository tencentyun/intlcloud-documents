## Overview
You can manage business origin servers by origin server group. The configured origin server group can be used by the [load balancing](https://intl.cloud.tencent.com/document/product/1145/46193) and [layer-4 proxy](https://intl.cloud.tencent.com/document/product/1145/46194) features as needed.
>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Origin-pull configuration** > **Origin server group** on the left sidebar.
2. On the origin server group page, select the target site and click **Create origin server group**.
3. On the origin server group creation page, configure relevant parameters and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/90df4b7dcce629406fcdd3608b5eb9ff.png)
**Parameter description:**
 - Origin server group name: Group name or description, which must be unique and can contain 1–200 letters, digits, underscores, and hyphens.
 - Configuration method: Currently, region- and weight-based load balancing options are supported. You can select one as needed.
  - Configuration by weight: Origin-pull by weight.
>?
>- The weight value range is 1–100.
>- If there is only one origin server address, the weight will be 100 by default and cannot be adjusted.
 - Configuration by region: Origin-pull by client IP region.
>?
>- **All regions** is the default global rule, which cannot be deleted and is required.
>- If multiple rules have the same region, the higher the rule position, the higher the priority.

## Configuration Limitations
- You can add up to 100 origin server addresses to a single origin server group but cannot enter IPv4 and IPv6 addresses together.
>!Currently, only certain nodes support IPv6 origin-pull.
- Port: Configurable port ranging from 1 to 65535.
- If an origin server group is used by [load balancing](https://intl.cloud.tencent.com/document/product/1145/46193), then:
 - If the proxy mode is **DNS only**, you cannot configure a port for origin server addresses or enter IPs and domains together as origin servers.
- If an origin server group is used by [layer-4 proxy](https://intl.cloud.tencent.com/document/product/1145/46194), then:
  - All origin server addresses must be configured with a port.
  - Configuration by region is not supported.
  - You can configure only one domain origin server but cannot enter it together with IP origin servers.
  - Currently, layer-4 proxy doesn't support IPv6 origin-pull. Therefore, IPv6 origin servers cannot be configured.
