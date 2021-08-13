## Type Overview
Tencent Cloud provides two types of cloud WAF, namely, SaaS WAF and CLB WAF. They have basically the same security protection capabilities but different connection methods and use cases. You can select an appropriate WAF type based on your actual deployment.

| Type     | SaaS WAF                                                      | CLB WAF                                                   |
| :------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| Use case | It is suitable for all users (Tencent Cloud users and local IDC users) and can be connected through domain names by means of DNS resolution and scheduling. | It is suitable for Tencent Cloud users who are using or plan to use layer-7 CLB.                 |
| Strength | It is widely applicable to users in and outside Tencent Cloud.             | <li>Imperceptible connection to WAF with millisecond-level latency is implemented, which does not require adjustment of your existing network architecture. <li>Website business forwarding and security protection are isolated from each other, and quick bypass is supported, ensuring that your website business is secure, stable, and reliable. <li>Multi-region connection is supported. |
| How to choose | If you need to protect both Tencent Cloud-hosted and local websites or layer-7 CLB is not used for your Tencent Cloud resources, you are recommended to use SaaS WAF. | If you are using or plan to use layer-7 CLB and have requirements for web security protection, bot behavior management, CCPC protection, or website security operation, you are recommended to use CLB WAF. |
| Region | You need to select a region when purchasing SaaS WAF                          | You need to select a region in the console after purchasing CLB WAF. |


## SaaS WAF
After you add a protected domain name and set the origin-pull information on WAF, it will assign a unique CNAME address to the protected domain name. You can modify the DNS resolution to change the original A record to the CNAME record and schedule traffic to the protected domain name to the WAF cluster, which will detect and block malicious traffic and forward normal traffic to the real server in order to protect your website security.
![](https://main.qcloudimg.com/raw/727094cc272c7cca426589a3ddcd6a2a.jpg)

## CLB WAF
By configuring a domain name, WAF can be connected to a layer-7 CLB (listener) cluster to detect threats in HTTP/HTTPS traffic passing through CLB and cleanse malicious traffic so as to separate business request forwarding from security protection, which minimizes the affect of security protection on your website business and thus ensures stable website operation.
![](https://main.qcloudimg.com/raw/1a31c507e5a508f15a48171e95252fc4.jpg)
CLB WAF provides two traffic processing modes:

- **Mirror mode**: associated with WAF through a domain name, CLB mirrors traffic to the WAF cluster, which performs bypass detection and alarming but does not return the request credibility status.
![](https://main.qcloudimg.com/raw/8c083a87ee4836b0efb6f8c6d296db31.png)
- **Cleansing mode**: associated with WAF through a domain name, CLB mirrors traffic to the WAF cluster, which performs bypass detection and alarming and synchronizes the request credibility status. Then, the CLB cluster will block or allow the requests based on their status.
![](https://main.qcloudimg.com/raw/215014fde2b779c8ba4427f61de20cb2.png)


