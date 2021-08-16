## What is Web Application Firewall?

Tencent Cloud Web Application Firewall (WAF) is an AI-based, one-stop web service protection solution. It uses the AI+ rules dual engine to identify malicious traffic and improve website security and reliability. In addition, it performs BOT behavior analysis to protect against malicious access behaviors and ensure the security of core services and data of websites.
WAF provides SaaS-based WAF and load-balanced WAF. These 2 types provide basically the same security protection capabilities but different access methods.
- SaaS-based WAF resolves a domain name to the CNAME address provided by the WAF cluster through DNS resolution. The IP address of the real server is configured through the WAF service. SaaS-based WAF cleanses and filters out malicious domain name traffic and returns legitimate traffic to the real server to ensure website security.
- Load-balanced WAF works with the Tencent Cloud Load Balancer cluster to mirror load-balanced HTTP/HTTPS traffic to the WAF cluster. WAF performs bypass threat detection and cleansing and then synchronizes the trusted status of user requests to the Tencent Cloud Load Balancer cluster to block threats and pass legitimate requests, helping ensure the security of websites.

The WAF service can effectively prevent SQL injection, cross-site scripting (XSS), trojan upload, unauthorized access, and other OWASP attacks. In addition, it can provide all-round protection for website systems and services by effectively filtering out CC attacks, providing zero-day vulnerability patches, and preventing web page tampering.

## Key features

<style>
table th:first-of-type {
    width: 180px;
}
</style>

| Feature                  | Description                                                         |
| --------------------- | ------------------------------------------------------------ |
| AI+ web application firewall | With the web attack identification based on AI+ rules, anti-bypass, low false negative, and low false positive, this service can precisely and effectively defend against common web attacks, such as SQL injection, unauthorized access, XSS, cross-site request forgery (CSRF), Webshell trojan upload, and other OWASP top 10 web security threats and attacks. |
| Virtual patching for zero-day vulnerabilities     | The Tencent security team provides 24/7 monitoring to uncover and respond to vulnerabilities. It distributes virtual patches for high-risk web vulnerabilities and zero-day vulnerabilities within 24 hours upon detection. Protected users can obtain the defense capability against emergency vulnerability and zero-day vulnerability attacks without performing any operation. The response cycle is significantly shortened. |
| Anti-tampering of web pages            | Users can cache core web page content to the cloud and publish cached web pages for substitution. This helps to protect organizations against the negative consequences caused by web page tampering. |
| Data leakage prevention            | WAF provides ex-ante server application hiding, real-time intrusion prevention, and ex-post sensitive data replacement and hiding policies to prevent backend databases from being hacked. |
| Defense against CC attacks           | WAF provides intelligent defense against CC attacks, and performs intelligent decision-making to generate defense policies based on the exceptional responses (timeout and response delay) of the real server and big data analysis of website behaviors. In addition, it provides multi-dimensional, custom, and precise access control, human-machine identification, frequency control, and other countermeasures to efficiently filter out unwanted access and mitigate CC attacks. |
| Crawler BOT behavior management     | Based on the AI+ rules repository, WAF provides web page crawler and BOT robot management to help enterprises mitigate business risks caused by malicious BOT behaviors. Business risks include website user data leakage, content infringement, competitive pricing, inventory query, black hat SEO, and business strategy disclosure. |
| 30-line BGP IP access protection | WAF supports dedicated 30-line BGP IP link access for defense nodes. The nodes are scheduled intelligently, which effectively solves the access delay problem and ensures the site access speed of users in all tiers of cities. This helps to deploy imperceptible cloud WAF security protection without affecting the website access speed. |

## Why do we need WAF?

In the following scenarios, the WAF service can provide effective defense and prevention against risks, and ensure system and business security of enterprise websites.

- **Data leakage (leakage of core information assets)**
  For many enterprises, websites are typically used as the entries to information assets. Hackers can steal enterprise information assets by means of web intrusion, resulting in incalculable losses to enterprises.
- **Malicious access and data crawling (data manipulation by business opponents causes service unavailable)**
  Hackers use zombie computers to launch CC attacks on the web server. As a result, the resources available are exhausted and the server fails to respond normally. Malicious users capture the core content of websites (literature blogs, recruitment sites, forum sites, and e-commerce site comments) through web crawling. Product details on e-commerce websites are scraped deliberately by competitors for research. Speculators seek for arbitrage by searching for low-price product information or obtaining marketing intelligence in advance.
- **Website malicious code and tampering (affecting the credibility and image)**
  After obtaining permissions of websites or servers, attackers inject malicious code to make users execute malicious programs, to earn traffic, to steal accounts, or to show off. They insert links of illicit content, and tamper with web page images and texts. These behaviors severely influence the operation of websites and impair the image and credibility of website operators.
- **Framework vulnerabilities (frameworks attacked during the patch fixing period)**
  Many web systems are based on common open-source frameworks, such as Structs2, Spring, and WordPress, which often carry security vulnerabilities. It is a tough and dangerous period before patches are ready to use, because many attacks spring up soon after the vulnerabilities are uncovered.

- **Service interruption caused by large traffic DDoS attacks**
  As a cheap and easy-to-use attack means, DDoS attacks are often used to disrupt the business operation of competitors or to make key portals inaccessible, leading to significant impact on business continuity and branding. Operators are often very passive when their websites are attacked.
