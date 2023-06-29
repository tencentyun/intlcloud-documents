This guide helps you prevent extra costs from extensive bandwidth and traffic caused by attacks and hotlinking. Note that such costs cannot be waived or refunded.

## Access Control

Enable access control (free of charge) for your domain names in the console.

| Item                                                   | Description                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Hotlink protection](https://intl.cloud.tencent.com/document/product/228/6292) | Configure a policy based on the referer field in the HTTP request header |
| [IP blocklist/allowlist](https://intl.cloud.tencent.com/document/product/228/6298) | Set up a policy based on requester IPs |
| [IP access limit](https://intl.cloud.tencent.com/document/product/228/6420) | Apply upper limits on the number of access requests/second/node from a client IP, which can help defend against high-frequency CC attacks and hotlinking. |
| [Authentication configuration](https://intl.cloud.tencent.com/document/product/228/35237) | Require the client to calculate the signature as configured and add it to the request. The CDN node allows the request only when the signature is authenticated. |
| [UA blocklist/allowlist](https://intl.cloud.tencent.com/document/product/228/37256) | Check the `User-Agent` of the HTTP request header and allow/reject requests according to the configured blocklist/allowlist. |
| [Downstream speed limit](https://intl.cloud.tencent.com/document/product/228/37257) | Control the CDN downstream bandwidth by setting the maximum throughput speed of a URL on the server. |

## Traffic Management

Set up policies for traffic and bandwidth control, monitor the traffic and bandwidth and get alerts in time.

| Item                                                   | Description                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Usage limit](https://intl.cloud.tencent.com/document/product/228/7541) | You can set a traffic/bandwidth usage limit for your domain name. When the traffic/bandwidth generated within a 5-minute period exceeds the limit, the CDN service will be suspended, returning 404 to all incoming requests. |
| [Cloud Monitor](https://console.cloud.tencent.com/monitor/overview) | Cloud Monitor helps monitor your CDN domain names and traffic usage. It also supports alerting via SMS, email and WeChat if the usage threshold is reached, allowing you to spot potential risks in a timely manner. |
| [Traffic packs](https://console.cloud.tencent.com/cdn/package)  | If you choose traffic-based billing, set the alert policies in **Traffic Pack Management**. You will be notified when the remaining traffic quota goes below the threshold. |

## Security Protection

You can also activate SCDN to further enhance the security of your service. It helps defeat cyber attacks in all round by using DDoS cleansing, CC adaptive identification, intelligent WAF protection and bot analysis.

For domain names connected to Tencent Cloud CDN, you can enable SCDN easily to keep your business away from web, DDoS and CC attacks.

| Feature         | Description                                                     |
| :--------------- | :----------------------------------------------------------- |
| Distributed cleansing | Backed by cache nodes around the world and the high-performance cleansing module, this feature defends against various traffic attacks such as SYN, TCP and ICMP floods by accurately cleansing them using an advanced feature recognition algorithm. |
| CC attack identification    | Adopts patented intelligent CC attack identification and blocking technologies. Combining the default blocking policies and custom rules, users can filter out malicious access requests by configuring the frequency and traffic limit. |
| Intelligent WAF protection    | Identify malicous access requests from bad ones and protecting your real server against web attacks including SQL injection, XSS attacks and local file inclusion in real time. With the self-developed AI engine incorporating Tencent's billion-level threat intelligence, a more accurate and effective identification and blocking of web threats can be implemented. |
| Bot analysis     | Analyzes all acceleration requests, identifying good bots from bad ones. Custom policies are supported. It provides a bot library covering various known bots from ads, screenshot tools, search engines, site monitoring and link querying. |
| Advanced access control     | Set up access control policies by more fields, such as client IP, URI, Referer, User-Agent and Params. Rules can also be tailored to different scenarios by setting a combination of conditions (equal to, include or exclude). |

