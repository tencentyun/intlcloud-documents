Anycast CLB is a load balancing service that supports cross-region dynamic acceleration. The Anycast CLB VIP is published in multiple regions. The client connects to the nearest POP and forwards access traffic to a CVM instance through Tencent Cloud IDC high-speed internet.
Anycast CLB can optimize network transfer and achieve multi-entry nearby access, reducing network jitter and packet loss. It improves the service quality of applications on the cloud, expands the service scope, and streamlines backend deployment.
>?This feature is currently in beta test. To try it out, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## What is Anycast?
Anycast means that when the same IP publishes a route in multiple locations simultaneously, the routing algorithm will deliver user traffic to the nearest router.
Advantages of Anycast CLB:
- **Low latency**
Anycast CLB publishes the VIP to multiple regions simultaneously via Anycast. Based on the transfer protocol, the request package arrives at the optimal VIP publishing region to gain privileged access to Tencent Cloud. It then accesses CVM through Tencent Cloud private network, avoiding public network traffic and reducing latency.
- **Reduced jitter and packet loss**
The transmission instability of cross-border public networks can result in network jitter and packet loss, undermining the service experience. By contrast, Anycast CLB boasts high transmission stability. It gives client requests nearby access to Tencent Cloud and enables cross-region transmission via Tencent Cloud dedicated private network connection, helping eliminate jitter and packet loss.
- **High reliability**
Transfer over the public network can be unreliable. When ISP linkage issues result in inaccessible services, users generally can only wait for services to resume. With Anycast CLB, Tencent Cloud private network, ISP networks, and Tencent Cloud POPs can achieve multi-entry and multi-path network to eliminate failures caused by a single region or connection, improving network stability.
- **Simplified deployment**
When clients are distributed across regions and need nearby access, servers need to be deployed in multiple regions and DNS must be configured to achieve load balancing. Because IPs vary by regions, the deployment is very complicated. With Anycast CLB, region attributes are converged at the IP level, eliminating the need to configure IPs for every region. Moreover, only one set of business logic needs to be maintained on the backend, and requests from different regions are directly routed to real servers through private network acceleration.


## Anycast CLB architecture
Anycast CLB architecture is as shown below:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
The VIP of Anycast CLB is published to multiple regions. The client connects to the nearest POP and forwards access traffic in an ultra-fast manner to a CVM instance over Tencent Cloud private network.

### Anycast Publishing Region
An Anycast publishing region is where an accelerated IP address is published, i.e., the POP where Anycast CLB VIP is published. The client accesses the nearest POP. Currently, Anycast CLB supports simultaneous publishing in the following regions: Beijing, Shanghai, Guangzhou, Hong Kong (China), Toronto, Silicon Valley, Frankfurt, Virginia, Moscow, Singapore, Seoul, Mumbai, Bangkok, and Tokyo.

### Anycast CLB Region
Just like a region of generic CLB instances, an Anycast CLB region is the one you selected when purchasing an Anycast CLB instance or the region where your real server resides. Currently, Anycast CLB is available in most regions.
- Asia Pacific: Beijing, Shanghai, Guangzhou, and Hong Kong (China), Singapore, Seoul, Mumbai, Bangkok, and Tokyo.
- Europe and North America: Toronto, Silicon Valley, Frankfurt, Virginia, and Moscow.

>?
>- The anycast capability of Anycast CLB is implemented by binding an Anycast EIP to a private network CLB instance.
>- Anycast EIP can be bound to private network CLB instances but not classic private network CLB or classic network CLB instances.
>

## Anycast CLB use cases

### Same server in multiple regions
If you are in the gaming industry, you may hope that the players from different regions are in the same server region or that your branches in different regions can share the same IDC. With the help of Anycast CLB, you can deploy real servers in one region (such as Guangzhou). You can purchase an Anycast CLB instance in that region and select the publishing regions as needed. In this way, players or employees in different regions can have nearby access to the same set of real servers.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Game Acceleration
Anycast CLB has been widely used in gaming acceleration. Through Anycast CLB, game requests can have nearby access to Tencent Cloud and get to game servers through Tencent Cloud private network, greatly shortening the public network path and reducing problems such as delay, jitter, and packet loss. Compared to the traditional acceleration, Anycast CLB requires no extra deployment of traffic receivers at the entry and eliminates the need for zoning, thus simplifying DNS deployment.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Operation Guide
### Prerequisites
This feature is currently in beta test. Make sure that the [application ticket](https://console.cloud.tencent.com/workorder/category) you submitted has been approved before using it.

### Directions
1. Log in to the [EIP console](https://console.cloud.tencent.com/cvm/eip?rid=1), select a region in the top-left corner of the **EIP** page, and click **Apply**.
4. In the **Apply for EIP** pop-up window, select **Acceleration IP** as the IP address type, set the bandwidth limit cap, click **I agree to Tencent Cloud EIP Service Agreement and Overdue Payment Policy**, and click **OK**.
4. Log in to the [CLB console](https://console.cloud.tencent.com/clb), select a region in the top-left corner of the **Instance Management** page, select the target private network CLB instance in the instance list, and click **More** > **Bind EIP** in the **Operation** column.
>?For the restrictions on binding EIP to private network CLB, see [Use Limits](https://intl.cloud.tencent.com/document/product/214/44336).
5. In the **Bind EIP** pop-up window, select the accelerated IP created just now and click **Submit**.
![]()
5. The private network CLB instance can provide Anycast CLB service after bound to an accelerated Anycast IP. For more information on CLB configuration, see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
![](https://main.qcloudimg.com/raw/f8e1334deb5679de7b5330208782a5e4.png)


## Relevant Documentation
[Binding Private Network CLB to EIP](https://intl.cloud.tencent.com/document/product/214/44336)