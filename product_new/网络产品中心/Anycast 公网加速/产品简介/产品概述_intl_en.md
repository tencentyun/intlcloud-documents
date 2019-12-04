## What is Tencent Cloud Anycast Internet Acceleration?
Anycast Internet Acceleration (AIA) is a global dynamic acceleration network that can greatly improve the internet access experience of your business. Different from other acceleration services at the application layer, it is capable of achieving network transfer optimization and multi-entry nearby access while reducing network jitter and packet loss, which can ultimately increase the service quality of your in-cloud applications, expand their service scope, and streamline backend deployment.

## Why Tencent Cloud AIA?
### Low latency
AIA publishes an IP to multiple regions simultaneously by means of Anycast. According to the transfer protocol, a request package will arrive at the optimal IP publishing region to gain privileged access to Tencent Cloud and then get to the CVM instance through Tencent Cloud private network, avoiding public network congestion and reducing latency.

### High reliability
Transmission over public networks can be unreliable. When ISP-specific line problems make services inaccessible, users generally have to wait until services are resumed. With the aid of AIA, Tencent Cloud private network, ISP networks, and Tencent Cloud POPs can achieve multiple network paths and entries to eliminate failures caused by single region or line and improve network stability.

### Reduced jitter
The instability of cross-border or cross-region public networks can result in network jitter, undermining the service experience. By contrast, AIA gives client requests nearby access to Tencent Cloud and enables cross-region transmission via Tencent Cloud Direct Connect, helping eliminate jitter and achieve high transmission stability.

### Simplified deployment
When your clients are distributed across regions and need nearby access, you have to deploy servers in all of those regions and configure DNS to achieve load balancing, and the IPs vary by region, making the deployment even more complicated. Through AIA, the region attribute is converged at the IP level, eliminating the need to configure IPs for every region. Moreover, you only need to maintain one set of business logic in the backend, and requests from different regions are directly routed to real servers through Direct Connect acceleration.

### Global load balancing
An IP can be published to multiple regions simultaneously with Anycast, and a request packet will arrive at the optimal IP publishing region (usually the nearest one) according to the transfer protocol, thereby achieving global load balancing. When a traffic attack occurs, as the IP has been published to multiple regions, the attacking traffic will be distributed.
#### Ease of use
AIA can be made compatible with common IP operations just by purchasing an accelerated EIP. It is simple to use and supports customizing the limit on public network bandwidth, which makes it easier for you to configure an appropriate bandwidth limit depending on costs or server processing speed. Plus, it features traffic monitoring for convenient issue traceability and analysis, and supports binding and unbinding operations to help you make changes to backend resources conveniently.

## Version history

| Update Date | Description |
|---------|---------|
| November 23, 2017 | Accelerated EIP of Anycast is released in beta test, and multi-region Anycast is supported |
| January 20, 2016 | Cross-region traffic scheduling is supported on the backend |

