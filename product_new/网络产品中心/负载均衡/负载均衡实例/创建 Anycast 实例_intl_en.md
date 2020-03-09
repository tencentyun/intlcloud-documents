CLB supports creating Anycast CLB instances. Anycast CLB is a load balancing service that supports global dynamic acceleration. CLB VIP is published in multiple regions around the world. The client connects to the nearest POP and forwards access traffic to CVM through the high-speed internet of Tencent Cloud IDC.
Anycast CLB can optimize network transfer and achieve multi-entry nearby access, reducing network jitter and packet loss. It improves the service quality of applications on the cloud, expands the service scope, and streamlines backend deployment.
>This feature is currently in beta test. To apply for a trial, submit an application for beta test eligibility.

## What is Anycast?
Anycast means that when the same IP publishes a route in multiple locations simultaneously, the routing algorithm will deliver user traffic to the nearest router.
Advantages of Anycast CLB:
- **Low latency**
Anycast CLB publishes the VIP to multiple regions simultaneously via Anycast. Based on the transfer protocol, the request package arrives at the optimal VIP publishing region to gain privileged access to Tencent Cloud. It then accesses CVM through Tencent Cloud private network, avoiding public network traffic and reducing latency.
- **Reduced jitter and packet loss**
Cross-region and cross-border public network linkage has unstable transfer performance, resulting in network jitter and packet loss that undermine user experience. In contrast, Anycast CLB has stable transfer performance. It gives client requests nearby access to Tencent Cloud and enables cross-region transfer via Tencent Cloud Direct Connect, eliminating jitter and packet loss.
- **High reliability**
Transfer over the public network can be unreliable. When ISP linkage issues result in inaccessible services, users generally can only wait for services to resume. With Anycast CLB, Tencent Cloud private network, ISP networks, and Tencent Cloud POPs can achieve multi-entry and multi-path network to eliminate failures caused by a single region or connection, improving network stability.
- **Simplified deployment**
When clients are distributed across regions and need nearby access, servers need to be deployed in multiple regions and DNS must be configured to achieve load balancing. Because IPs vary by regions, the deployment is very complicated. With Anycast CLB, region attributes are converged at the IP level, eliminating the need to configure IPs for every region. Moreover, only one set of business logic needs to be maintained on the backend, and requests from different regions are directly routed to real servers through private network acceleration.

## Anycast CLB architecture
Anycast CLB architecture is as shown below:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
The VIP of Anycast CLB will be published in multiple regions around the world. The client connects to the nearest POP and forwards access traffic to CVM over the high-speed Tencent Cloud private network.

### Anycast publishing region
Anycast publishing region is where an accelerated IP address is published, i.e., POP where VIP of Anycast CLB is published. The client accesses the nearest POP. Currently, Anycast CLB supports simultaneous publishing in the following regions: Beijing, Shanghai, Guangzhou, Hong Kong (China), Toronto, Silicon Valley, Frankfurt, Virginia, Moscow, Singapore, Seoul, Mumbai, Bangkok, and Tokyo.

### Anycast CLB region
Same as the region of CLB instance, Anycast CLB region is the region you selected when purchasing an Anycast CLB or the region where the real server resides. Currently, Anycast CLB is available in most regions.
- China: Beijing, Shanghai, Guangzhou, and Hong Kong.
- Europe and the North America: Toronto, Silicon Valley, Frankfurt, Virginia, and Moscow.
- Southeast Asia: Singapore, Seoul, Mumbai, Bangkok, and Tokyo.
>Anycast CLB does not support Classic CLB.

## Anycast CLB use cases
### Unified server for global access
Customers from the game industry may hope that global players in different regions are on the same server (or an enterprise may hope that its global office branches share the same IDC). With Anycast CLB, real servers can be deployed in one region (such as Guangzhou). You can purchase an Anycast CLB in Guangzhou region and select publishing regions as needed. Global game players (or company employees) can then have nearby access to the same set of real servers.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Game Acceleration
Anycast CLB has been widely used in game acceleration. With Anycast CLB, game requests have nearby access to Tencent Cloud and can access game servers through Tencent Cloud private network, shortening the public network path and reducing problems such as delay, jitter, and packet loss. Compared to traditional acceleration, Anycast CLB does not need to deploy extra devices at the entry to receive traffic nor differentiate regions, simplifying DNS deployment.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Operation Guide
### Prerequisites
>This feature is currently in beta. First ensure that your application for beta test eligibility has been approved.
### Directions
1. Log into the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the left sidebar, click **[EIP](https://console.cloud.tencent.com/cvm/eip2)** to enter the "EIP Management" page.
3. Click **Apply for EIP**. In the pop-up window, select **Accelerated IP** as the IP address type and **CLB** as the object to be bound, and click **OK**.
4. Log into the [CLB Console](https://console.cloud.tencent.com/clb), select a private network CLB (Classic CLB instance is not supported), and click **More** > **Bind Accelerated IP** in the "Operation" column.
5. The private network CLB instance can provide Anycast CLB service after bound to an accelerated IP. For more information on CLB configuration, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
