## Overview
Load balancing dynamically optimizes origin-pulls and intelligently assigns traffic to effectively avoid failed origin servers and reduce origin server overloads, ensuring the availability of the entire service.
>?
>- Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
>- Load balancing can be by region or weight.


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Origin-pull configuration** > **Load balancing** on the left sidebar.
2. On the load balancing page, select the target site and click **Create load balancing task**.
3. On the load balancing creation page, configure the relevant parameters and click **Submit task**.
![](https://qcloudimg.tencent-cloud.cn/raw/e4838d99b76850735b926395b5d75181.png)
**Parameter description:**
 - Hostname: Site acceleration domain, which is also the specific site domain at the origin server IP accessed during origin-pull, i.e., origin-pull domain. You can select an existing domain pulled from DNS records or add a domain (which must be under the current site).
>!
>- Currently, the business acceleration domain and the origin-pull domain must be the same.
>- If `Hostname` conflicts with an existing DNS record, the configuration in load balancing has a higher priority and will overwrite that in the DNS record. If the load balancing task is deleted, the original DNS record will recover.
 - Proxy mode: Select a mode as needed. For more information, see [Proxy Mode](https://intl.cloud.tencent.com/document/product/1145/45968).
>?If you select the **DNS only** mode and the connection method is NS connection, you can choose to configure the TTL.

 - Origin server: Configure load balancing origin servers by origin server group. You can select an existing origin server group or create one.
    - For more information on how to create an origin server group and configuration limits, see [Origin Server Group](https://intl.cloud.tencent.com/document/product/1145/46159).
    - If you select the **DNS only** mode, you can configure one origin server group at most.
    - If you select **proxy acceleration** or **secure acceleration**, you can configure two origin server groups at most, and requests will be forwarded to them by priority. Only when the origin server group whose priority is 1 fails and becomes unavailable will requests be forwarded to the group whose priority is 2. This implements the concept of primary/secondary origin server groups.
4. On the load balancing page, you can view a created task. Each task has a deployment status.
 - Deploying: The current load balancing task is being deployed and cannot be deleted. Wait patiently.
 - Effective: The current load balancing task has taken effect in the production network and cannot be deleted. You need to disable it first before you can delete it.
 - Ineffective: The current load balancing task is disabled.


## FAQs
### Why are some origin server groups grayed out during origin server configuration?
- The grayed out origin server group conflicts with the currently selected proxy mode; for example:
  - A port has been configured for an origin server in the origin server group, so the group cannot be used in **DNS only** mode.
  - The origin server group has an IPv6 origin server, so it cannot be used in **DNS only** mode.
  - The origin server group has both IP and domain origin servers, so it cannot be used in **DNS only** mode.
- The maximum number of configurable origin server groups is reached:
  - If you select the **DNS only** mode, you can configure one origin server group at most.
  - If you select the **proxy acceleration** or **secure acceleration** mode, you can configure two origin server groups at most.
