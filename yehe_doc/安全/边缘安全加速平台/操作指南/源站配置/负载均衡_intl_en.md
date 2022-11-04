## Overview
Load balancing dynamically optimizes origin-pulls and intelligently assigns traffic to effectively avoid failed origin servers and reduce origin server overloads, ensuring the availability of the entire service.
>? Load balancing can be performed by region or weight.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Origin Configuration** > **Cloud Load Balancer** on the left sidebar.
2. On the load balancing page, select the target site and click **Create load balancing task**.
3. On the load balancing creation page, configure the relevant parameters and click **Submit task**.
**Parameter description:**
 - Hostname: Domain name of a site, which is accessed on the origin server during origin-pull.
>!
>- To set an origin domain different from the acceleration domain when you bind a customer origin server, you can use [host header rewriting](https://intl.cloud.tencent.com/document/product/1145/46965) to rewrite the host header to the actual origin domain.
>- If the hostname conflicts with existing DNS records, the load balancing configuration takes higher priority and will overwrite the records in [Domain Name Service](https://intl.cloud.tencent.com/document/product/1145/46353).

 - Proxy mode: Set the proxy mode to **Proxied** or **Only DNS**.
    - Proxied: In this mode, EdgeOne deploys security or acceleration configuration for the host record (subdomain name) according to your plan.
    - Only DNS: In this mode, EdgeOne only provides DNS resolution.
 - TTL: If you set the proxy mode to "Only DNS" and access via NS, the TTL is configurable.
 - Origin group: Configure load balancing origin servers by origin group.
>!
>- If you select the **Only DNS** mode, you can configure one origin group at most.
>- If you select **Proxied**, you can configure two origin groups at most, and requests will be forwarded to them by priority. Only when the origin group whose priority is 1 fails and becomes unavailable will requests be forwarded to the group whose priority is 2. This implements the concept of primary/secondary origin groups.
>- Secondary object storage origin groups are not supported.

4. On the load balancing page, you can view a created task. Each task has a deployment status.
 - Deploying: The current load balancing task is being deployed and cannot be deleted.
 - Activated: The current load balancing task has taken effect and cannot be deleted. You need to disable it before deletion.
 - Deactivated: The current load balancing task is disabled.


## FAQs
### Why are some origin groups grayed out during origin server configuration?
- The grayed out origin group conflicts with the currently selected proxy mode in the following situations:
  - A port has been configured for an origin server in the origin group, so the group cannot be used in **Only DNS** mode.
  - The origin group has an IPv6 origin server, so it cannot be used in **Only DNS** mode.
  - The origin group has both IP and domain origin servers, so it cannot be used in **Only DNS** mode.
- The maximum number of configurable origin groups is reached:
  - If you select the **Only DNS** mode, you can configure one origin group at most.
  - If you select the **Proxied** mode, you can configure two origin groups at most.
- Private access is enabled for the object storage origin server:
  - Secondary object storage origin servers cannot be created currently.
