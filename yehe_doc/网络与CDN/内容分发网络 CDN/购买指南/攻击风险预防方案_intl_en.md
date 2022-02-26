<style> 
table th:nth-of-type(1) { width:20%; } 
table th:nth-of-type(2){ width:80%; } 
</style>




This guide will help you prevent extra costs from extensive bandwidth and traffic caused by malicious attacks and hotlinking.

## Access Control

You are recommended to enable access control (free of charge) for your domain names in the console to avoid wasting bandwidth.

| Item                                                   | Description                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Hotlink protection](https://intl.cloud.tencent.com/document/product/228/6292) | Configure an access control policy based on the value of the referer field in the HTTP request header, so as to restrict the the access sources and prevent malicious hotlinking. |
| [IP blocklist/allowlist](https://intl.cloud.tencent.com/document/product/228/6298) | By setting an access control policy based on requester IPs, you can restrict the access source to prevent malicious IP hotlinking and attacks. |
| [IP access limit](https://intl.cloud.tencent.com/document/product/228/6420) | By limiting the number of access requests per second from a client IP to a node, you can defend against high-frequency CC attacks and malicious hotlinking. |
| [Authentication configuration](https://intl.cloud.tencent.com/document/product/228/35237) | When the authentication is configured, the client needs to calculate the signature as configured and add it into a request sent to the server. The CDN node allows the request when the signature is authenticated. |
| [UA blocklist/allowlist](https://intl.cloud.tencent.com/document/product/228/37256) | Determines whether to allow a request based on the `User-Agent` of the HTTP request header. |
| [Downstream speed limit](https://intl.cloud.tencent.com/document/product/228/37257) | Controls the CDN downstream bandwidth by setting the maximum throughput speed of a URL on the server. |

## Traffic Management

You are recommended to enable traffic and bandwidth management for free to monitor the traffic and bandwidth usage of your domain name and receive alarm messages.

| Item                                                   | Description                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Bandwidth cap](https://intl.cloud.tencent.com/document/product/228/7541) | You can set up an upper limit for the bandwidth usage for your domain name. When the bandwidth generated in a sample period (5 minutes) exceeds the value you set, the requests will be forcibly forwarded to the origin server or CDN service will be suspended (a 404 error will be returned for all requests）to avoid extra bills. |
| [Monitoring](https://console.cloud.tencent.com/monitor/overview) | Cloud Monitor helps monitor your CDN domain names and traffic usage. It also supports alerting via SMS, email and WeChat if the usage threshold is reached, allowing you to spot potential risks in a timely manner. |
| [Traffic pack management](https://console.cloud.tencent.com/cdn/package)  | If you use the bill-by-traffic method, you can set the alarm policies in **Traffic Pack Management** in the console. An alarm message will be sent when the remaining traffic goes below the threshold. |

## Security Protection

To protect your business against potential attacks, you are recommended to enable SCDN. It helps defeat cyber attacks in all round by using DDoS cleansing, CC adaptive identification, intelligent WAF protection and bot analysis.

For domain names connected to Tencent Cloud CDN, you can enable SCDN easily to keep your business away from web, DDoS and CC attacks.

| Feature         | Description                                                     |
| :--------------- | :----------------------------------------------------------- |
| Distributed cleansing | Backed by over 1,100 qualified CDN nodes and the high-performance cleansing module, this feature defends against various traffic attacks such as SYN, TCP and ICMP floods by accurately cleansing them using an advanced feature recognition algorithm. A single node leveraging Tencent Cloud's Anti-DDoS data centers can defeat up to 1 Tbps of DDoS attacks. |
| CC attack identification    | Adopts patented intelligent CC attack identification and blocking technologies. Combining the default blocking policies and custom rules, users can filter out malicious access requests by configuring the frequency and traffic limit. |
| Intelligent WAF protection    | This feature, based on Tencent's massive web attack samples, supports identifying good access requests from bad ones and protecting your real server against web attacks including SQL injection, XSS attacks and local file inclusion in real time. With the self-developed AI engine incorporating Tencent's billion-level threat intelligence, a more accurate and effective identification and blocking of web threats can be implemented. |
| Bot analysis     | Integrating with Tencent Cloud’s AI-based WAF rules, this feature supports analyzing acceleration requests, identifying good bots from bad ones and managing custom rules. It provides a bot library covering various known bots from ads, screenshot tools, search engines, site monitoring and link querying, and an unique AI technology for user behavior modeling and determining the source of abnormal traffic. |
| Advanced access control     | In addition to basic rules defined based on IP, Referer and UA blocklist/allowlist, this feature supports creating a complex access control rule by specifying fields such as client IP, URI, Referer, User-Agent and Params. Users can also he rule can also be tailored to different application scenarios by setting a combination of conditions (equal to, include or exclude). |


