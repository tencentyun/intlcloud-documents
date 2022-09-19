## WAF Overview

Web Application Firewall (WAF) is a one-stop AI-based risk prevention solution for web business operations. It can identify malicious traffic with the aid of AI and rule engines to protect websites and further improve the website security and reliability. By leveraging bot behavior analysis, it can defend against malicious access requests and safeguard core website businesses and data.
Tencent Cloud provides two types of on-cloud WAF, namely, SaaS WAF and CLB WAF. They have basically the same security protection capabilities but different connection methods.
 - SaaS WAF resolves a domain name to the CNAME address provided by the WAF cluster through DNS and configures the real server IP through WAF. In this way, malicious traffic is cleansed and filtered, and normal traffic is forwarded to the real server, protecting the website security.
 - CLB WAF works with the Tencent Cloud CLB cluster to mirror the HTTP/HTTPS traffic of CLB instances to the WAF cluster. Then, WAF performs bypass threat detection and cleansing and syncs the trusted status of user requests to the CLB cluster, which will block or allow the requests accordingly to protect the website security.

WAF can effectively prevent SQL injection, cross-site scripting (XSS), trojan upload, unauthorized access, and other OWASP attacks. In addition, it can also provide all-around protection for website systems and businesses by effectively filtering CC attacks, providing zero-day vulnerability patches, and preventing webpage tampering.    

## Key Features

<style>
table th:first-of-type {
    width: 180px;
}
</style>

| Feature                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| AI + WAF   | Web attack recognition is based on AI + rules. It is anti-bypass and low in both false negative and false positive rates. Web attack recognition defends effectively against common web attacks, including the OWASP top 10 web security threats (SQL injection, unauthorized access, cross-site scripting, cross-site request forgery, web shell trojan upload, etc). |
| Virtual zero-day vulnerability patching     | The 24\*7 monitoring service from Tencent security team identifies and responds to vulnerabilities proactively. Within 24 hours, it issues virtual patches to zero-day and high-risk web vulnerabilities. Protected users can get zero-day and emergency vulnerability protection instantly and automatically, shortening vulnerability response time dramatically. |
| Web tampering protection            | You can cache core web contents to the cloud and publish cached web pages. This acts like a substitute and can prevent negative consequences of web page tampering. |
| Data leakage protection            | Backend data is well protected by pre-event server and application concealing, mid-event attack prevention, and post-event sensitive data replacement and concealing. |
| CC attack protection           | Smart CC protection intelligently generates defense policies based on the real server's abnormal responses (such as timeout and response delay) and website behavior big data analysis. It supports multidimensional custom accurate access control, intelligently and effectively filters malicious access requests, and defends against CC attacks with measures such as CAPTCHA and frequency control. |
| Crawler and bot traffic management     | The AI + rules-based webpage crawler and bot management feature help you avoid business risks caused by malicious bot behaviors, including website user data leakage, content infringement, competing price comparison, inventory search, malicious SEO, and business strategy leakage. |
| 30 BGP lines for access protection | With its 30 dedicated BGP lines for protective nodes, WAF supports smart node scheduling to effectively solve the issues with access delay to ensure high access speed in metropolises and small towns. It implements cloud-based security protection without compromising the website access speed. |

## Why WAF

WAF can effectively protect website systems and businesses of enterprises in the following use cases.

- **Data leakage (leakage of core information assets)**
  A website is the entry to enterprise information assets and may be hacked for asset theft, causing incalculable losses to enterprises.
- **Malicious access and data crawling (unavailability and data utilized by competitors)**
  Hackers control botnets to launch CC attacks on a website, which will consume all its resources and makes it unavailable. Malicious users scrape core content of websites (blog, recruitment, forum, and ecommerce websites) by using web crawlers. For example, ecommerce offering details are crawled by competitors for analysis, and low-price offering information is crawled or promotion intelligence is obtained before sales campaigns by bargain hunters for their benefits.
- **Network trojans and tampering (affecting credibility and image)**
  After obtaining website or server permissions, attackers can inject malicious code to make users execute malicious programs, drive traffic, steal accounts, and show off. They may also implant links to pornographic, gambling, and illegal information or tamper with the images and texts on the website, adversely affecting website operations, undermining the credibility, and damaging the image.
- **Framework vulnerability (attacks during patching)**
  Many web systems are based on common open-source frameworks such as Structs 2, Spring, and WordPress, which are prone to security vulnerabilities. A lot of attacks will emerge just one day after the vulnerabilities are discovered, making patching extremely hard.
- **Business interruption due to high-traffic DDoS attacks**
  DDoS attacks have become a cost-effective and easy way to interrupt the business of competitors or make their key portals inaccessible. These attacks have severe impact on business continuity and brand image. More often than not, companies are very passive when attacked.

