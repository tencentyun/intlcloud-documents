## Overview
You can manage business origin servers by origin group. The configured origin group can be used by the [load balancing](https://intl.cloud.tencent.com/document/product/1145/46193) and [layer-4 proxy](https://intl.cloud.tencent.com/document/product/1145/46194) features as needed.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Origin Configuration** > **Origin Group** on the left sidebar.
2. On the origin server group page, select the target site and click **Create origin group**.
3. On the origin group creation page, configure relevant parameters and click **Create**.
![](https://qcloudimg.tencent-cloud.cn/raw/90df4b7dcce629406fcdd3608b5eb9ff.png)
**Parameter description:**
 - Group name: Origin group name or description, which must be unique and can contain 1–200 letters, digits, underscores, and hyphens.
 - Origin type: Type of the origin server, which can be customer origin, object storage origin, or Tencent Cloud COS.
    - Customer origin: It is the customer's origin server storing business resources, which can be an IP or a domain name.
    - Object storage origin: It is a third-party object storage origin server, which is a bucket address for which private access can be enabled. Now only Amazon Web Services S3 is supported.
    - Tencent Cloud COS: Select a Tencent Cloud COS bucket under the current account as origin.
 - Configuration method: If you select **Customer origin** as the origin type, you can select:
   - Configure by weight: Origin-pull by weight.
>?
>- If there is only one origin server, the weight is set to 100 by default and cannot be adjusted.
>- If there is more than one origin server, specify weights in the range 1-99.

  - Configure by region: Origin-pull by client IP region.
>?
>- **All** is the default global rule, which cannot be deleted.
>- If multiple rules have the same region, the higher the rule position, the higher the priority.

  - Configure by HTTP protocol: Origin-pull by the HTTP protocol of the client request.
>?Configure at least one origin address for the HTTPS and HTTP protocols respectively.

## Customer origin configuration restrictions
- You can add up to 100 origin server addresses to a single origin server group but cannot enter IPv4 and IPv6 addresses together.
>!Currently, only certain nodes support IPv6 origin-pull.

- Port number: Specify a port in the range 1-65535.
- If an origin group is used by [load balancing](https://intl.cloud.tencent.com/document/product/1145/46193), then:
 - If the proxy mode is **Only DNS**, you cannot configure a port for origin server addresses or enter IPs and domains together as origin servers.
- If an origin group is used by [L4 proxy](https://intl.cloud.tencent.com/document/product/1145/46194), then:
  - All origin server addresses must be configured with a port.
  - **Configure by region** and **Configure by HTTP protocol** are not supported.
  - You can configure only one domain origin server but cannot enter it together with IP origin servers.
  - Currently, L4 proxy doesn't support IPv6 origin-pull. Therefore, IPv6 origin servers cannot be configured.
