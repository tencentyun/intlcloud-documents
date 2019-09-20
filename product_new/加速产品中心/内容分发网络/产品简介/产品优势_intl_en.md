## Stable Acceleration and Global Presence
**Nodes deployed in Mainland China**
Tencent Cloud CDN has deployed more than 1,100 cache nodes across Mainland China, covering major ISPs such as China Mobile, China Unicom, and China Telecom, as well as small and mid-sized ISPs like China Mobile Tietong and Great Wall Broadband Network. With a total node bandwidth of over 80 Tbps and reserved bandwidth of over 120 Tbps, CDN solves the problems of high access latency and instability due to factors such as geographical distribution, network, and origin server performance, helping you deliver your content to users more efficiently.
![](https://mc.qcloudimg.com/static/img/19f5708498e59acef7d60a755dee686e/image.png)
**Overseas nodes**
Tencent Cloud CDN has deployed over 200 overseas nodes in more than 50 countries and regions to help your business go global seamlessly.
![](https://main.qcloudimg.com/raw/3afd00dab2b8095717794777bfd66b98.png)

## Intelligent Scheduling and Linkage Optimization
When your user requests for resources, the request may not be transmitted over the optimal access route due to such factors as network, geographical location, and bandwidth. Through real-time monitoring of the linkage across the entire network and leveraging Tencent Cloud's proprietary GSLB scheduling system and intelligent routing technology, Tencent Cloud CDN optimizes the user access experience in the following ways.

**Optimal connection**
Through Tencent Cloud's proprietary GSLB scheduling system, the request by your user will be routed to the optimal CDN node closest to them to ensure fast access to the requested resource. After the accelerated domain name is connected, the system will schedule the nodes dynamically based on access conditions to better serve your business needs.

**Optimal origin-pull**
If the request is scheduled to a node which has not cached the requested resource, the node needs to go back to the origin server to get the resource. Based on real-time status monitoring over the entire network and the intelligent routing technology, Tencent Cloud CDN selects the optimal origin-pull linkage to ensure rapid access to the resource.

**Dynamic acceleration**
Dynamic requests such as logins cannot be accelerated through nodes; instead, they need to be directly transmitted to the origin server through transparent transmission. Tencent Cloud CDN provides optimal network linkages for such requests to bypass poor-quality and congested linkages and increases the speed by 20%.

## High Security and Reliability and Transparent Access
In a public network that involves relatively high security risks, your origin server may be subject to network attacks, making it unable to serve your users or causing potential losses due to unauthorized use of your published resources. Tencent Cloud CDN safeguards your business in an all-round way with the aid of the following security features.

**Access control**
Tencent Cloud CDN supports a range of access control policies and allows you to configure features such as referer blacklist/whitelist, IP blacklist/whitelist, IP access limit, and timestamp-based hotlink protection as needed to prevent unauthorized use of your resources.

**HTTPS support**
Tencent Cloud CDN supports HTTPS transfer on all nodes across the entire network. If your business requires high security and has a certificate, the certificate can be directly uploaded to the CDN nodes for deployment. Both user requests sent to a node and origin-pull requests will be encrypted to ensure data security. If you don't have a certificate, Tencent Cloud can provide you with a third-party DV certificate for free, which can be deployed with speed and ease to make connections more secure.

**Domain hijacking prevention**
To avoid domain hijacking during resolution that may make the domain unable to be resolved to the optimal access node, Tencent Cloud CDN offers an HTTP DNS direct connection solution, which allows your domain to be resolved quickly through a public DNS and protects it from hijacking.

## Simple Connection and Diversified Management Tools
To connect to Tencent Cloud CDN, you do not need to adjust or change your business, worry about that you cannot obtain the business statistics and consumption details in a transparent manner, or monitor business status in real time. Tencent Cloud CDN features quick and simple connection and comes with a wide variety of management tools, so that the entire CDN service can be presented in the most possible transparent way.

**Simple connection**
To connect to Tencent Cloud CDN, you only need to provide your domain name. CDN will assign you a CNAME in a fixed format, and you need to modify the corresponding CNAME configuration at your domain name service provider. Once the DNS takes effect, you can start using the acceleration service.

**Statistics monitoring**
Tencent Cloud CDN provides multi-dimensional data analytics, including statistics of consumption, access, request status, and origin server. For real-time monitoring of such statistics, you can go to [Cloud Monitor](https://intl.cloud.tencent.com/product/cm) to configure relevant alarms, helping you stay up to date on your business status. Tencent Cloud CDN also provides monthly operations reports to keep you informed of monthly business changes.

**Diversified management tools**
You can manage domain names in the CDN Console, such as modifying configurations, activating, deactivating or deleting domain names. You can also query all types of statistical graphs. Tencent Cloud CDN offers a wide variety of APIs for custom monitoring, data display, and data analytics to facilitate OPS of your business.
## Results Comparison
The figure below is a comparison in latency and availability between origin servers using Tencent Cloud CDN and those not. As you can see, Tencent Cloud CDN reduces latency by about 78% and increases resource availability to over 99.5%.
![](https://mc.qcloudimg.com/static/img/f3f9a16b4ccd0b863509a496b45249d4/image.png)
The above results are based on the benchmarking test method commonly used in the industry. For detailed test data and results, see [CDN Performance Test](https://intl.cloud.tencent.com/doc/product/228/1198).
