CLB supports creating Anycast CLB instances. Anycast CLB is a load balancing service that supports global dynamic acceleration. The CLB VIP is published in multiple regions around the world. The client connects to the nearest POP and forwards access traffic to a CVM instance through Tencent Cloud IDC high-speed internet.
Anycast CLB can achieve network transfer optimization and multi-entry near access and reduce network jitter and packet loss. It can ultimately improve the service quality of in-cloud applications, expand the service scope, and streamline the backend deployment.
> This feature is currently in beta. <!-- [Submit an application]() if you want to use it.-->

## What is Anycast?
Anycast means that when the same IP publishes a route in multiple locations simultaneously, the routing algorithm will deliver user traffic to the nearest router.
Advantages of Anycast CLB:
- **Low latency**
Anycast CLB publishes the VIP to multiple regions simultaneously by means of Anycast. According to transfer protocol, a request package will arrive at the optimal VIP publishing region to gain privileged access to Tencent Cloud and then get to the CVM instance through Tencent Cloud private network, avoiding public network congestion and reducing latency.
- **Reduced jitter and packet loss**
The transmission instability of cross-carrier or cross-border public networks can result in network jitter and packet loss, undermining the service experience. By contrast, Anycast CLB boasts a high transmission stability. It gives client requests a near access to Tencent Cloud and enables cross-region transmission via Tencent Cloud private network connection, helping eliminate jitter and packet loss.
- **High reliability**
Transmission over public networks can be unreliable. When ISP-specific line problems make services inaccessible, users generally have to wait until services are resumed. With the aid of Anycast CLB, Tencent Cloud private network, ISP networks, and Tencent Cloud POPs can achieve multiple network paths and entries to eliminate failures caused by single region or line and improve network stability.
- **Simplified deployment**
When your clients are distributed across regions and need near accesses, you have to deploy servers in all of those regions and configure DNS to achieve load balancing. And the IPs vary by region, making the deployment even more complicated. Through Anycast CLB, the region attribute is converged at the IP level, eliminating the need to configure IPs for every region. Moreover, you only need to maintain one set of logic in the backend, and requests from different regions are directly routed to real servers through private network acceleration.

## Anycast CLB Architecture
The Anycast CLB architecture is as shown below:
![](https://main.qcloudimg.com/raw/22e2999156768fa7866b70001280fce5.png)
The VIP of Anycast CLB is published to multiple regions around the world. The client connects to the nearest POP and forwards access traffic in an ultra-fast manner to a CVM instance over Tencent Cloud private network.

### Anycast Publishing Region
An Anycast publishing region is where an accelerated IP address is published, i.e., the POP where Anycast CLB VIP is published. The client accesses the nearest POP. Currently, Anycast CLB supports the following publishing regions:
- Publishing region A: covering China, Europe, and the North America, where VIP is published simultaneously to Beijing, Shanghai, Guangzhou, Hong Kong (China), Toronto, Silicon Valley, Frankfurt, Virginia, and Moscow.
- Publishing region B: covering China and Southeast Asia, where VIP is published simultaneously to Beijing, Shanghai, Guangzhou, Hong Kong (China), Singapore, Seoul, Mumbai, Bangkok, and Tokyo.

### Anycast CLB Region
Just like a region of generic CLB instances, an Anycast CLB region is the one you selected when purchasing an Anycast CLB instance or the region where your real server resides. Currently, Anycast CLB is available in most regions.
- China: Beijing, Shanghai, Guangzhou, and Hong Kong (China).
- Europe and the North America: Toronto, Silicon Valley, Frankfurt, Virginia, and Moscow.
- Southeast Asia: Singapore, Seoul, Mumbai, Bangkok, and Tokyo
>
>- Anycast CLB supports **CLB** but not Classic CLB.
>- Anycast CLB supports **layer-4 protocols (TCP/UDP)** but not layer-7 protocols (HTTP/HTTPS) currently.
>- Currently, Anycast CLB does not support S4, SN3ne, S2ne, M4, or GN6s CVM instances.

## Anycast CLB Use Cases
### Unified Server for Global Access
If you are in the gaming industry, you may hope that the players from different corners of the world are on the same server or that your branches around the globe can share the same IDC. With the help of Anycast CLB, you can deploy real servers in one region (such as Guangzhou). Purchase an Anycast CLB instance in that region, and select the publishing regions as needed. In this way, players or employees in different parts of the world can have near access to the same set of real servers.
![](https://main.qcloudimg.com/raw/548f5853d5d56af85a248d5ee64d2c39.png)

### Gaming Acceleration
Anycast CLB has been widely used in gaming acceleration. Through Anycast CLB, game requests can have near access to Tencent Cloud and get to game servers through Tencent Cloud private network, greatly shortening the public network path and reducing problems such as delay, jitter, and packet loss. Compared to the traditional acceleration, Anycast CLB requires no extra deployment of traffic receivers at the entry and eliminates the need of zoning, thus simplifying DNS deployment.
![](https://main.qcloudimg.com/raw/c1db004b30c41a6c0968e95a2197332b.png)


## Operation Guide
### Creating an Anycast CLB Instance
1. To apply for beta test, log in at Tencent Cloud's official website and go to the [CLB purchase page](https://buy.cloud.tencent.com/lb).
2. Select **CLB** as instance type and select **Enable Anycast Accelerated IP** for the accelerated IP. Other configurations are the same as [general instance configurations](http://intl.cloud.tencent.com/document/product/214/8975).
3. After purchase, return to the [CLB instance list page](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) where you can view the Anycast CLB instance you just purchased.


### Using an Anycast CLB Instance
1. Log in to the [CLB Console](https://console.cloud.tencent.com/loadbalance/index?rid=1&forward=1) and go to the "CLB instance list".
2. Click an instance ID to enter the details page.
3. On the **Listener Management** tab, you can configure listeners, set forwarding rules, and bind CVM instances. For more information, see [Getting Started with CLB](http://intl.cloud.tencent.com/document/product/214/8975).

