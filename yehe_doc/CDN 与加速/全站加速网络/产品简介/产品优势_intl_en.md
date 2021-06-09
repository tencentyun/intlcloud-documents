Tencent Cloud Enterprise Content Delivery Network (ECDN) has the strengths below:

## Mesh-like Interconnection and Global Acceleration
**Nodes in the Chinese mainland**
To allow your published content to reach users faster, Tencent Cloud has set up more than 2,000 ECDN nodes across the nation, covering mainstream ISPs such as China Mobile, China Unicom, and China Telecom as well as many medium and small-sized ISPs such as China Tietong and Great Wall Broadband. Mesh-like interconnection is implemented between cache nodes, and a huge number of transmission linkages are available.
![](https://main.qcloudimg.com/raw/487228cdfb5666b34edab2242db7c3c0.jpg)

**Nodes outside the Chinese mainland**
Tencent Cloud has been working industriously on global acceleration since 2017. As of May 2021, Tencent Cloud has over 800 cache nodes across more than 70 countries and regions with a total reserved bandwidth of over 40 Tbps, helping your business go global with ease and speed.


## One-stop Acceleration for Dynamic and Static Contents
For origin servers with dynamic resources such as ASP and PHP files and static resources such as text, images, audios, and videos, ECDN can deliver convenient data access and efficient data transmission.

**Intelligent cache**
You can configure cache rules for static contents on edge servers, and the corresponding contents can be returned to requesters directly.

**Origin-pull optimization**
For scenarios where dynamic contents are pulled from the origin server, ECDN dynamically schedules requests and adopts the optimal origin-pull path, guaranteeing access speed.

## Dynamic Scheduling and Optimal Linkage
When requesting resources, your users may be faced up with problems of high delay and high packet loss due to such factors as network, region, or bandwidth. ECDN, through the real-time monitoring of the linkages across the network and by using the self-developed Global Server Load Balance (GSLB) scheduling system and intelligent routing technology, optimizes user's access experience in the following three ways.

**Optimal connection**
With Tencent Cloud's GSLB scheduling system, your users' requests will be allocated to the nearest, optimal cache node to connect to the acceleration network.

**Optimal linkage**
ECDN selects the optimal network linkage for the requests to effectively bypass linkages with poor quality or congested linkages, to ensure rapid access to the content based on the real-time status monitoring across network and intelligent routing technology.

**Protocol optimization**
ECDN has independently developed an optimized algorithm for the protocol layer, which makes full use of the bandwidth resources to make the network transmission more stable and improve the network performance.

## Secure, Stable, and Reliable
In a complex public network environment, your origin server may fail to serve when suffers packet loss caused by network jitters or attacks from hackers. ECDN comprehensively safeguards your businesses in the following two aspects:

**Private protocol**
When a user requests for a connection to the acceleration network, you can use a reliable Tencent private protocol for transmission through private network to ensure security.

**Redundancy transmission**
ECDN supports multi-linkage redundancy transmission, to guarantee the reliability of data transmission, so that users can enjoy a reliable web experience.

## One-click Connection and Transparency in Business
Using ECDN is easy. You do not need to adjust your businesses, worry about not having clear business statistics and consumption details, or monitor business status in real time. ECDN features quick and simple connection and comes with a wide variety of management tools, presenting you with a comprehensive overview of the entire ECDN service.

**Simple connection**
To use the ECDN service, you only need to provide your domain name, and ECDN will assign you a standard CNAME. You then need to add a corresponding CNAME record at your domain name service provider to finish the service connection. You can use ECDN right after the DNS resolution takes effect.

**Statistics monitoring**
ECDN provides multi-dimensional data analysis for you to understand user requests. If you want to monitor the real-time data, you can use [Cloud Monitor](https://console.cloud.tencent.com/monitor) to configure related alarms to keep track of your businesses.

**Diversified management tools**
You can perform domain name management, setting changes, going online/going offline, deletion and other operations through the ECDN console. You can also make queries on the above statistics and charts.
