[//]: # (DOCID:XXXXX)
[//]: # (status:pendingtranslate; TAPDID:XXXXXXX;)
[//]: # (status:published; TAPDID:XXXXXXX; publishdate:20181225)
[//]: # (publishlink: https://intl.cloud.tencent.com/document/product/436)
[//]: # (doctag: price,EIP, operation, API)

Leveraging Tencent's over a decade of experience in security accumulated from various lines of business, Tencent Cloud Aegis Anti-DDoS is a multi-layer, all-around, cost-effective protection solution against DDoS attacks for your business. It is capable of precise purge of various types of network attack traffic and directing of normal traffic to business servers, preventing business fluctuations, service interruptions and user experience downgrading caused by potential DDoS attacks. In addition, it features protective resources at the Tbps level and customizable advanced security policies for targeted protection against specific attack behaviors.
[//]: # (pendingaddlink: doc:docid)
[//]: # (refdoc:docid)

## Product Categories
Aegis Anti-DDoS offers the following options: [DDoS protective IP](https://intl.cloud.tencent.com/document/product/685/20368) and [DDoS protection pack](https://intl.cloud.tencent.com/document/product/685/20369) which are paid services; [advanced anti-DDoS policy](https://console.cloud.tencent.com/gamesec/asp), [advanced HTTP anti-CC defense policy](https://console.cloud.tencent.com/gamesec/ccsp) and [watermark protection](https://console.cloud.tencent.com/gamesec/mark) which can be configured free of charge. 
 
## Pricing
Aegis Anti-DDoS uses a mixed billing model including prepaid and pay-per-use on a daily basis. Base protection bandwidth is prepaid on a monthly basis, while elastic protection bandwidth and forwarded business traffic are pay-per-use on a daily basis. For detailed pricing of Aegis Anti-DDoS, see:

- **[Single-IP Pricing for DDoS Protective IP](https://intl.cloud.tencent.com/document/product/685/15262)**
- **[Package Pricing for DDoS Protective IP](https://intl.cloud.tencent.com/document/product/685/19025)**
- **[Single-IP Pricing for DDoS Protection Pack](https://intl.cloud.tencent.com/document/product/685/15266)**
- **[Multi-IP Pricing for DDoS Protection Pack](https://intl.cloud.tencent.com/document/product/685/15267)**

## **How to Use**
Tencent Cloud Aegis Anti-DDoS has web-based UIs (i.e. console). If you have already signed up for a Tencent Cloud account, you can log in to the [Aegis Anti-DDoS Console](https://console.cloud.tencent.com/gamesec) to purchase and perform various operations.

## Related Concepts
The following concepts are usually involved in Aegis Anti-DDoS:
- **DDoS**
This is short for distributed denial-of-service, a network attack technique that uses network resources to initiate service requests to specific target servers and makes end user's normal service requests impossible to be completed by exhausting the bandwidth or other resources of the target servers.
- **IP blocking**
 If the DDoS attack traffic exceeds the protection bandwidth set by the user, Aegis Anti-DDoS will block all service requests to the attacked target servers for a period of time.
- **BGP network**
This is the type of network directly connected to the Internet AS using the Border Gateway Protocol (BGP). Tencent Cloud's BGP links are connected to 28 ISPs, eliminating cross-network latency and enabling an excellent network access experience.
- **China Telecom, China Unicom and China Mobile networks**
This refers to the non-BGP networks of China Mobile, China Unicom and China Telecom. They provide static IP resources, and non-local users need cross-network access when using these resources.
- **Forwarding rule**
This is to configure the rule according to which the business request first accesses the protective IP's service port and then is forwarded to the real server port of the real server IP address. Port forwarding rules can be configured and real server polling by weight or by minimum number of connections is supported.
- **Traffic-forwarding egress IP address**
This is the exit IP address used when forwarding the business request from the protective IP to the real server. If relevant security policies are configured for the real server, the exit IP address should be added to the whitelist to avoid mistaking normal requests for attacks.
- **Protection bandwidth**
This is divided into base protection bandwidth and elastic protection bandwidth. If optional elastic protection is chosen, the protection bandwidth is the highest bandwidth that can protect against the actual attacks. If the attack traffic exceeds the protection bandwidth, the system will temporarily block the attacked IPs.
- **Region**
This refers to the region where a protective IP or protection pack is available. It is recommended to choose the region closest to the real server. Protection pack can only be bound to the Tencent Cloud public IP addresses in the same region where it is available.

## **Related Services**
- **DDoS protective IP**
This is a large-traffic DDoS protection service for Tencent Cloud customers (including off-cloud servers). The protective IP is used as the access point for the business traffic. The backend protection system checks the traffic and performs traffic purges if any DDoS attacks are detected, and then forwards the normal business request to the real server of the business.
- **Protected domain name**
Protected domain name is provided free of charge when the user creates a business in the console. The user can configure the CNAME of their primary domain name to resolve to the protected domain name for easy access. Resolution to the protective IP can be enabled for the protected domain name for smart resolution based on request source.
- **DDoS protection pack**
This is an enhanced DDoS protection service for Tencent Cloud customers' in-cloud servers. It works in single-IP or multi-IP mode. Single-IP protection pack can be bound to one Tencent Cloud public IP, while multi-IP protection pack can be bound to multiple Tencent Cloud public IPs.
- **Elastic traffic pack**
DDoS protection pack is billed based on the elastic protection traffic, and when the attacks exceed the base protection and trigger elastic protection, the incurred elastic traffic will be deducted from a purchased elastic traffic pack in the same region. Compared with billing by the elastic bandwidth, it can effectively cope with peak-type high-bandwidth attacks with lower protection costs.
