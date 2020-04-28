Tencent Cloud Enterprise Content Delivery Network (ECDN) has the following strengths:
## Meshed Interconnection and Global Acceleration
**Nodes in Mainland China**
Tencent Cloud has deployed more than 1,100 ECDN nodes across Mainland China, covering major ISPs such as China Mobile, China Unicom, and China Telecom, as well as small and mid-sized ISPs like China Mobile Tietong and Great Wall Broadband Network. With cache nodes interconnected in a meshed manner a high number of transfer linkages, ECDN helps you deliver your content to users more efficiently.
![](https://main.qcloudimg.com/raw/487228cdfb5666b34edab2242db7c3c0.jpg)

**Nodes outside Mainland China**
ECDN has over 200 overseas nodes deployed in more than 50 countries and regions to help your business go global seamlessly.


## One-Stop Acceleration for Dynamic/Static Resources
Your resources on origin servers usually include dynamic content (.asp, .php, etc.) and static content (text, image, audio/video, etc). ECDN can conveniently and efficiently accelerate data transfer for sites with both dynamic and static resources at one stop.

**Intelligent caching**
You can customize the rules for caching static content on edge servers. When users access the content, edge servers will directly return the required content.

**Origin-pull optimization**
For origin-pull of dynamic content, ECDN can select and allocate the optimal origin-pull route with dynamic scheduling so as to ensure high origin-pull speed.

## Dynamic Scheduling and Optimal Linkage Selection
When your user requests resources, problems such as high latency and high packet loss rate may occur due to such factors as network, geographical location, and bandwidth. Through real-time monitoring of the linkages across the entire network and leveraging Tencent Cloud's proprietary Global Server Load Balance (GSLB) scheduling system and intelligent routing technology, ECDN optimizes the user access experience in the following ways:

**Optimal connection**
Through Tencent Cloud's proprietary GSLB scheduling system, requests made by your users will be routed to the optimal cache node closest to them so as to connect to ECDN.

**Optimal linkage**
Based on real-time status monitoring over the entire network and the intelligent routing technology, ECDN can select the optimal network linkage to effectively bypass poor-quality and congested linkages, enabling fast access to the requested resources.

**Protocol optimization**
ECDN's proprietary protocol-layer optimization algorithm can make full use of bandwidth resources, which helps improve the network transfer stability and network performance.

## High Security and Reliability
In a complex public network, your origin server may be subject to problems such as packet loss due to network jitters and hacker attacks, making it unable to serve your users properly. ECDN safeguards your business in an all-round way with the aid of the following security features:

**Private protocol**
When a user request reaches ECDN, it is transferred over the private network with the reliable Tencent's private protocol, which guarantees the security.

**Redundant transfer**
ECDN supports multi-linkage redundant transfer to ensure data transfer reliability, helping your business deliver a reliable web experience.

## Quick Connection and Business Transparency
Using ECDN is easy. You do not need to perform any business configurations, provide any business statistics and consumption details, or monitor business status in real time. ECDN features quick and simple connection and comes with a wide variety of management tools, presenting you with a comprehensive overview of the entire ECDN service.

**Easy connection**
To connect to ECDN, you only need to provide your domain name. ECDN will assign you a CNAME address in a fixed format, and you need to add the corresponding CNAME record at your domain name service provider to connect to ECDN. Once the DNS takes effect, you can start using ECDN.

**Statistics monitoring**
ECDN provides multi-dimensional data analysis, so that you can have a comprehensive view on user requests to your business. For real-time monitoring of such statistics, you can go to [Cloud Monitor](https://console.cloud.tencent.com/monitor) to configure relevant alarms that help you stay up to date on your business status.

**Diversified management features**
You can manage domain names in the ECDN Console, such as activating, deactivating, or deleting domain names as well as modifying their configurations. You can also query all types of statistics in graphs and charts.