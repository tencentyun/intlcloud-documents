## Stable Acceleration and Global Presence
**Nodes deployed in Mainland China**
Tencent Cloud CDN has more than 1,100 cache nodes deployed across Mainland China, covering major ISPs such as China Mobile, China Unicom, and China Telecom, as well as small and mid-sized ISPs like China Mobile Tietong and Great Wall Broadband Network. With a total node bandwidth of over 80 Tbps and reserved bandwidth of over 120 Tbps, CDN solves high access latency and instability issues due to factors such as geographical distribution, network, and origin server performance, helping you deliver your content to users more efficiently.
![](https://main.qcloudimg.com/raw/487228cdfb5666b34edab2242db7c3c0.jpg)
**Overseas Nodes**
Tencent Cloud CDN has over 200 overseas nodes deployed in more than 50 countries and regions to help your business go global seamlessly.
![](https://main.qcloudimg.com/raw/034a95d5f46fb8bf848c0a53dd265611.png)

## Intelligent Scheduling and Linkage Optimization
When your user requests for resources, the request may not be transmitted over the optimal access route due to such factors as network, geographical location, and bandwidth. Through real-time monitoring of the linkage across the entire network and leveraging Tencent Cloud's proprietary GSLB scheduling system and intelligent routing technology, Tencent Cloud CDN optimizes the user access experience in the following ways.

**Optimal Connection**
Through Tencent Cloud's proprietary GSLB scheduling system, the request by your user will be routed to the optimal CDN node closest to them to ensure fast access to the requested resource. After the accelerated domain name is connected, the system will schedule the nodes dynamically based on access conditions to better serve your business needs.

**Optimal Origin-pull**
If the request is scheduled to a node which has not cached the requested resource, the node needs to get the resource from the origin server. Based on real-time status monitoring across the entire network and the intelligent routing technology, Tencent Cloud CDN selects the optimal origin-pull linkage to ensure rapid access to the resource.

**Dynamic Acceleration**
Dynamic requests such as logins cannot be accelerated through nodes; instead, they need to be directly transmitted to the origin server through transparent transmission. Tencent Cloud CDN provides optimal network linkages for such requests to bypass poor-quality and congested linkages, increasing the speed by 20%.

## High Security and Transparent Access
In a public network susceptible to high security risks, your origin server may be subject to network attacks, resulting in service interruptions or potential losses due to unauthorized use of your published resources. Tencent Cloud CDN provides comprehensive protection for your business with the following security features.

**Access Control**
Tencent Cloud CDN supports a range of access control policies and allows you to configure features such as referer blacklist/whitelist, IP blacklist/whitelist, IP access limit, and timestamp-based hotlink protection to prevent unauthorized use of your resources.

**HTTPS Support**
Tencent Cloud CDN supports HTTPS transfer on all nodes across the entire network. If your business has high security requirements and has a certificate, the certificate can be directly uploaded to the CDN nodes for deployment. Both user requests sent to a node and origin-pull requests will be encrypted to ensure data security. If you don't have a certificate, Tencent Cloud can provide you with a free third-party DV certificate, which can be deployed easily to quickly secure connections.

**Domain Hijacking Prevention**
To avoid domain hijacking during resolution where the domain will not be resolved to the optimal access node, Tencent Cloud CDN offers an HTTP DNS direct connection solution. This solution allows your domain to be resolved quickly through Public DNS and protects it from hijacking.

## Simple Connection and Diversified Management Tools
Using Tencent CDN is easy. You do not need to undergo any business configurations,  provide any business statistics and consumption details, or monitor business status in real time. Tencent Cloud CDN features quick and simple connection and comes with a wide variety of management tools, presenting you with a comprehensive overview of the entire CDN service.

**Simple Connection**
To connect to Tencent Cloud CDN, you only need to provide your domain name. CDN will assign you a CNAME in a fixed format, and you need to modify the corresponding CNAME configuration at your domain name service provider. Once the DNS takes effect, you can start using the acceleration service.

**Statistics Monitoring**
Tencent Cloud CDN provides multi-dimensional data analytics, including data statistics such as consumption, access, request status, and origin server. You can go to [Cloud Monitor](https://intl.cloud.tencent.com/product/cm) to configure alarms for real-time monitoring of such statistics to help you stay up to date on your business status. Tencent Cloud CDN also provides monthly operations reports to keep you informed of monthly business changes.

**Diversified Management tools**
You can manage domain names in the CDN Console and perform operations such as modifying configurations, activating, deactivating or deleting domain names. You can also query all types of statistical graphs. Tencent Cloud CDN offers a wide variety of APIs for custom monitoring, data display, and data analytics to facilitate OPS of your business.
## Results Comparison
The figure below is a comparison in latency and availability between origin servers using Tencent Cloud CDN and those not. As you can see, Tencent Cloud CDN reduces latency by about 78% and increases resource availability to over 99.5%.
![](https://main.qcloudimg.com/raw/e3fac66f19c6c9b481d4897115e07f33.jpg)
The above results are based on the benchmarking test commonly used in the industry. For detailed test data and results, see [CDN Performance Test](https://intl.cloud.tencent.com/doc/product/228/1198).
