## Overview
Load balancing dynamically optimizes origin-pulls and intelligently assigns traffic to effectively avoid failed origin servers and reduce origin server overloads, ensuring the availability of the entire service.
>? Load balancing can be performed by region or weight.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Origin Configuration** > **Cloud Load Balancer** on the left sidebar.
2. On the load balancing page, select the target site and click **Create load balancing task**.
3. On the load balancing creation page, configure the relevant parameters and click **Submit task**.
**Parameter description:**
 - Hostname: Domain name of a site, which is accessed on the origin server during origin-pull.
>!
>- To set an origin domain different from the acceleration domain when you bind a customer origin server, you can use [host header rewriting](https://intl.cloud.tencent.com/document/product/1145/46965) to rewrite the host header to the actual origin domain.
>- If the hostname conflicts with existing DNS records, the load balancing configuration takes higher priority and will overwrite the records in [Domain Name Service](https://intl.cloud.tencent.com/document/product/1145/46353).

 - Proxy: **Proxy acceleration** or **Only DNS**.
    - Proxy acceleration: EdgeOne will automatically deliver security/acceleration configuration for the host record (subdomain name) according to your plan.
    - Only DNS: EdgeOne will only provide DNS resolution.
 - TTL: If you select **Only DNS** for **Proxy** and select **NS access**, the TTL is configurable.
 - Origin: If you select **Proxy acceleration** for **Proxy**, you can select primary/secondary origin-pull and advanced origin-pull configuration.
    - Primary/Secondary origin-pull: You can configure up to two origin groups, and requests will be forwarded to them by priority. Only when the origin group at priority 1 fails and becomes unavailable will requests be forwarded to the group at priority 2. This implements the concept of primary/secondary origin groups.
    - Advanced origin-pull configuration: You can configure the load balancing origin server based on the matched URL path.
>!
>- If you select the **Only DNS** mode, you can configure only one origin group.
>- If you select the **Proxy acceleration** mode, you can configure up to two origin groups, and requests will be forwarded to them by priority. Only when the origin group at priority 1 fails and becomes unavailable will requests be forwarded to the group at priority 2. This implements the concept of primary/secondary origin groups.
>- Secondary object storage origin groups are not supported.

4. On the load balancing page, you can view a created task. Each task has a deployment status.
 - Deploying: The current load balancing task is being deployed and cannot be deleted.
 - Running: The current load balancing task is taking effect in the production environment and cannot be deleted. You need to disable it before you can delete it.
 - Disabled: The current load balancing task is disabled.


## FAQs
### Why are some origin groups grayed out during origin server configuration?
- The grayed out origin group conflicts with the currently selected proxy mode in the following situations:
  - A port has been configured for an origin server in the origin group, so the group cannot be used in **Only DNS** mode.
  - The origin group has an IPv6 origin server, so the group cannot be used in **Only DNS** mode.
  - The origin group has both IP and domain origin servers, so it cannot be used in **Only DNS** mode.
- The maximum number of configurable origin groups is reached:
  - If you select the **Only DNS** mode, you can configure only one origin group.
  - If you select the **Proxy acceleration** mode, you can configure up to two origin groups.
- Grayed-out origin groups are object storage origin servers with private access enabled:
  - Secondary object storage origin servers cannot be created currently.
