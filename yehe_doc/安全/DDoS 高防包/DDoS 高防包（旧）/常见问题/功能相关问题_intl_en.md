### Does Anti-DDoS Pro support non-Tencent Cloud IPs?
No. Anti-DDoS Pro only provides DDoS protection for public IPs of Tencent Cloud. For protection of non-Tencent Cloud IPs, please [purchase Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/15483).

### What if the bound resource has expired but the Anti-DDoS Pro instance has not? 
An Anti-DDoS Pro instance is purchased by month, and provides protection based on IPs. If the resource protected by your Anti-DDoS Pro instance expires and you do not change the IP bound to the instance, the instance will continue to provide protection for the bound IP, but the resource corresponding to the IP may not be yours. It is recommended to renew your Tencent Cloud resources or change the IP you want to protect in time.


### Does Anti-DDoS Pro provide protection sevice for domain names?
No. For domain name protection and application-layer protection, please [purchase Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/15483).

### The protection bandwidth of Anti-DDoS Basic is 2 Gbps. If I purchase an Anti-DDoS Pro instance, will the final protection bandwidth be the sum of the two?
No. In such a case, the final protection bandwidth you enjoy will be the protection bandwidth of the Anti-DDoS Pro instance. The default protection bandwidth of Anti-DDoS Basic will not be added to it.
For example, a CVM IP has a free protection bandwidth of 2 Gbps. If you purchase a 20 Gbps Anti-DDoS Pro instance for it, the maximum protection capability the CVM IP enjoys is 20 Gbps.

### What’re the differeces between Anti-DDoS Pro and Anti-DDoS Advanced? 
- Protection coverage:
 -  Anti-DDoS Pro provides DDoS protection only for services within Tencent Cloud.
 -  Anti-DDoS Advanced can protect non-Tencent Cloud resources, including non-Tencent Cloud service IPs and domain names.
- Access:
  - Anti-DDoS Pro is easy to access and you do not need to change your public IPs.
  - To access Anti-DDoS Advanced, you need to modify DNS or your business IPs.

## What are the differences between Anti-DDoS Pro and non-BGP protection?
|     Differences     | Anti-DDoS Pro             | Non-BGP Protection                  |
| -------- | -------------------- | ------------------- |
| Access Costs | Low access costs without the need of changing your server IPs | Complicated configuration where you need to replace your server IPs with non-BGP IPs and enter the domain name and port information |
| Access Quality | Uses BGP bandwidth and offers a lower access latency across networks and 30% higher access speed         | No BGP bandwidth with a high network latency and poor quality                              |
| Pricing | Flexible pricing that supports sharing and a combination of base and elastic protection                              | Complicated pricing where you need to pay for traffic|   

