## Overview
Load balancing dynamically optimizes origin-pulls and intelligently directs traffic away from failed origins. This can reduce origin overloads and ensure service availability.
>? Load balancing can be performed by region or weight.

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Origin Settings** > **Load Balancing** on the left sidebar.
2. On the load balancing page, select the target site and click **Create load balancing task**.
3. On the load balancing creation page, configure the relevant parameters and click **Submit task**.

**Parameter description:**
 - **Hostname**: Domain name of a site, which is accessed on the origin during origin-pull.
>!
>- To set an origin domain different from the acceleration domain when you bind a custom origin, you can use [host header rewriting](https://intl.cloud.tencent.com/document/product/1145/46965) to rewrite the host header to the actual origin domain.
>- If the hostname conflicts with existing DNS records, the load balancing configuration takes higher priority and will overwrite the records in [Domain Service](https://intl.cloud.tencent.com/document/product/1145/46353).

 - **Proxy mode**:
    - **Proxied**: In this mode, EdgeOne deploys security or acceleration configuration for the host record (subdomain name) according to your plan.
 -  **Origin**:
    - **Primary/Secondary origin-pull**: You can configure up to two origin groups, and requests will be forwarded to them by priority. Only when the origin group at priority 1 fails and becomes unavailable will requests be forwarded to the group at priority 2. This implements the concept of primary/secondary origin groups.
    - **Advanced origin-pull configuration**: You can configure the load balancing origin server based on the matched URL path.
>!
>- In the **Proxied** mode, you can configure two origin groups at most, and requests will be forwarded to them by priority. Only when the origin group whose priority is 1 fails and becomes unavailable will requests be forwarded to the group whose priority is 2. This implements the concept of primary/secondary origin groups.
>- Private bucket origins cannot be configured as secondary origin groups.

4. On the load balancing page, you can view a created task. Each task has a deployment status.
 - Deploying: The current load balancing task is being deployed and cannot be deleted.
 - Running: The current load balancing task has taken effect and cannot be deleted. You need to disable it before deletion.
 - Disabled: The current load balancing task is disabled.

## FAQs
### Why are some origin groups grayed out?
- Reached the upper limit of origins in this group
  - Up to 2 origin groups can be configured.
- Private access is enabled for the bucket origin:
  - Private bucket origins cannot be configured as secondary origin groups.