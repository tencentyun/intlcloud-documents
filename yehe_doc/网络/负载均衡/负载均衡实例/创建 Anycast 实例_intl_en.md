CLB supports creating Anycast CLB instances. Anycast CLB is a load balancing service that supports cross-region dynamic acceleration. CLB VIP is published in multiple regions. The client connects to the nearest POP and forwards traffic to a CVM instance through the high-speed internet of Tencent Cloud IDC.
Anycast CLB can achieve network transfer optimization and multi-entry nearby access and reduce network jitter and packet loss, which can ultimately improve the service quality of in-cloud applications, expand the service scope, and streamline backend deployment.
>?This feature is currently in beta test. To apply for a trial, submit a ticket for beta test eligibility.

## What is Anycast?
Anycast means that when the same IP is published in multiple locations simultaneously, the routing algorithm will deliver user traffic to the nearest router.
Advantages of Anycast CLB:
- **Low latency**
Anycast CLB publishes the VIP to multiple regions simultaneously by means of Anycast. According to transfer protocol, a request package will arrive at the optimal VIP publishing region to gain privileged access to Tencent Cloud and then get to the CVM instance through Tencent Cloud private network, avoiding public network congestion and reducing latency.
- **Reduced jitter and packet loss**
The transmission instability of cross-border or cross-carrier public networks can result in network jitter and packet loss, undermining the service experience. By contrast, Anycast CLB boasts high transmission stability. It gives client requests nearby access to Tencent Cloud and enables cross-region transmission via Tencent Cloud dedicated private network connection, helping eliminate jitter and packet loss.
- **High reliability**
Transmission over public networks can be unreliable. When ISP-specific line problems make services inaccessible, users generally have to wait until services are resumed. With the aid of Anycast CLB, Tencent Cloud private network, ISP networks, and Tencent Cloud POPs can achieve multiple network paths and entries to eliminate failures caused by single region or line and improve network stability.
- **Simplified deployment**
When your clients are distributed across regions and need nearby access, you have to deploy servers in all of those regions and configure DNS to achieve load balancing, and the IPs vary by region, making the deployment even more complicated. Through Anycast CLB, the region attribute is converged at the IP level, eliminating the need to configure IPs for every region. Moreover, you only need to maintain one set of business logic on the backend, and requests from different regions are directly routed to real servers through private network acceleration.

## Anycast CLB Architecture
The Anycast CLB architecture is as shown below:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
The VIP of Anycast CLB is published to multiple regions around the world. The client connects to the nearest POP and forwards access traffic in an ultra-fast manner to a CVM instance over Tencent Cloud private network.

### Anycast publishing region
An Anycast publishing region is where an accelerated IP address is published, i.e., the POP where Anycast CLB VIP is published. The client accesses the nearest POP. Currently, Anycast CLB supports simultaneous publishing in the following regions: Beijing, Shanghai, Guangzhou, Hong Kong (China), Toronto, Silicon Valley, Frankfurt, Virginia, Moscow, Singapore, Seoul, Mumbai, Bangkok, and Tokyo.

### Anycast CLB region
Just like a region of generic CLB instances, an Anycast CLB region is the one you selected when purchasing an Anycast CLB instance or the region where your real server resides. Currently, Anycast CLB is available in most regions.
- China: Beijing, Shanghai, Guangzhou, and Hong Kong SAR.
- Europe and the North America: Toronto, Silicon Valley, Frankfurt, Virginia, and Moscow.
- Southeast Asia: Singapore, Seoul, Mumbai, Bangkok, and Tokyo.

>?
>- The anycast capability of Anycast CLB is implemented by binding an Anycast EIP to a private network CLB instance.
>- Anycast EIP can be bound to private network CLB instances but not classic private network CLB instances or classic network CLB instances.
>

## Anycast CLB Use Cases
### Unified server for cross-region access
If you are in the gaming industry, you may hope that the players from different places are in the same server region or that your branches around the globe can share the same IDC. You can use Anycast CLB to deploy real servers in one region (such as Guangzhou), purchase an Anycast CLB instance in that region and select the publishing regions as needed. In this way, players or employees can obtain the nearby access to the same real servers.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Gaming acceleration
Anycast CLB has been widely used in gaming acceleration. Through Anycast CLB, game requests can have nearby access to Tencent Cloud and get to game servers through Tencent Cloud private network, greatly shortening the public network path and reducing problems such as delay, jitter, and packet loss. Compared to the traditional acceleration, Anycast CLB requires no extra deployment of traffic receivers at the entry and eliminates the need for zoning, thus simplifying DNS deployment.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Operation Guide
### Prerequisites
>This feature is currently in beta. Make sure that your application for beta test eligibility has been approved before using it.
### Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. On the left sidebar, click **[EIP](https://console.cloud.tencent.com/cvm/eip2)** to enter the EIP management page.
3. Click **Apply**. In the pop-up window, select **Accelerated IP** as the IP address type and click **OK**.
![](https://main.qcloudimg.com/raw/838f629b9d40c4db3be1e98dbd95c7f3.png)
4. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), select a private network CLB instance (classic CLB instances are not supported), and click **More** > **Bind Accelerated IP** in the "Operation" column.
![](https://main.qcloudimg.com/raw/e4877ad575321d2599b3258cf741a8a3.png)
5. After the private network CLB instance is bound to an accelerated IP, it can provide Anycast CLB service. For more information on CLB configuration, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
![](https://main.qcloudimg.com/raw/f8e1334deb5679de7b5330208782a5e4.png)
