### Does Anti-DDoS Pro support non-Tencent Cloud IPs?
No. Anti-DDoS Pro only provides DDoS protection for public IPs in Tencent Cloud. If you need protection for IPs off Tencent Cloud, please purchase Anti-DDoS Advanced, which supports protection for website domain names and service ports.

### What if the bound resource has expired but the Anti-DDoS Pro instance has not? 
An Anti-DDoS Pro instance is purchased by month and provides protection based on IPs. If the resource protected by your Anti-DDoS Pro instance expires and you do not change the IP bound to the instance, the instance will continue to provide protection for the bound IP, but the resource corresponding to the IP may not be yours. You are recommended to renew your Tencent Cloud resources or change the protected IP in time.

### Does Anti-DDoS Pro provide protection service for domain names?
Supported. Anti-DDoS Pro only provides layer-7 CC protection for HTTP domain names. For more details, see [Domain Name Protection](https://intl.cloud.tencent.com/document/product/1029/36135).

### The protection bandwidth of Anti-DDoS Basic is 2 Gbps. If I purchase an Anti-DDoS Pro instance, will the final protection bandwidth be the sum of the two?
No. In such a case, the final protection bandwidth you enjoy will be the protection bandwidth of the Anti-DDoS Pro instance. The default protection bandwidth of Anti-DDoS Basic will not be added to it.
For example, if a CVM IP has a free protection bandwidth of 2 Gbps and you purchase an Anti-DDoS Pro instance for it, the maximum protection capability the CVM IP enjoys will be the maximum protection capability of the Anti-DDoS Pro instance in the current region.

### What are the differences between Anti-DDoS Pro and Anti-DDoS Advanced?
- Protected object:
 -  Anti-DDoS Pro provides DDoS protection only for services within Tencent Cloud.
 -  Anti-DDoS Advanced is for users both in and off Tencent Cloud and supports protection for website domain names and service ports.
- Access:
  - Anti-DDoS Pro is easy to access and you do not need to change your public IPs.
  - To access Anti-DDoS Advanced, you need to modify DNS or your business IPs.

### What are the differences between Anti-DDoS Pro and non-BGP protection?
|     Differences     | Anti-DDoS Pro             | Non-BGP Protection                  |
| -------- | -------------------- | ------------------- |
| Access costs | Low access costs without the need of changing your server IPs | Complicated configuration where you need to replace your server IPs with non-BGP IPs and enter the domain name and port information |
| Access quality | It uses BGP bandwidth and offers a lower access latency across networks and 30% higher access speed         | It has no BGP bandwidth with a high network latency and poor quality                              |
| Pricing policy | Billed according to the "number of protected IPs + protected times" with max protection available at no additional elastic costs | Billed in a complex manner with traffic fees incurred |

