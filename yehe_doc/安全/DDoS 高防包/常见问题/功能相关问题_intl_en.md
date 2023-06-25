### Does Anti-DDoS Pro support non-Tencent Cloud IPs?
No. Anti-DDoS Pro only provides DDoS protection for public IPs in Tencent Cloud. If you need protection for IPs off Tencent Cloud, purchase Anti-DDoS Advanced, which supports protection for website domain names and service ports.

### Does Anti-DDoS Pro provide protection service for VPN gateways?
Yes.

### Does Anti-DDoS Pro provide protection service for Anycast EIP?
Anycast EIP does not support access to Anti-DDoS Pro. If you need DDoS protection, please purchase [Anti-DDoS Advanced (Global Enterprise)](https://intl.cloud.tencent.com/document/product/297/41155) and then bind the Anycast EIP to the Anti-DDoS Advanced instance.



### What if the bound resource has expired but the Anti-DDoS Pro instance has not? 
An Anti-DDoS Pro instance is purchased by month, and provides protection based on IPs. If the resource protected by your Anti-DDoS Pro instance expires and you do not change the IP bound to the instance, the instance will continue to provide protection for the bound IP, but the resource corresponding to the IP may not be yours. It is recommended to renew your Tencent Cloud resources or change the IP you want to protect in time.


### The protection bandwidth of Anti-DDoS Basic is not exceeding 2 Gbps. If I purchase an Anti-DDoS Pro instance, will the final protection bandwidth be the sum of the two?
No. In such a case, the final protection bandwidth you enjoy will be the protection bandwidth of the Anti-DDoS Pro instance. The default protection bandwidth of Anti-DDoS Basic will not be added to it.
For example, if a CVM IP has a free protection bandwidth of not exceeding 2 Gbps and you purchase an Anti-DDoS Pro instance for it, the maximum protection capability the CVM IP enjoys will be the maximum protection capability of the Anti-DDoS Pro instance in the current region.

### What are the differences between Anti-DDoS Pro and Anti-DDoS Advanced?
- Protection coverage:
 -  Anti-DDoS Pro provides DDoS protection only for services on Tencent Cloud.
 -  Anti-DDoS Advanced is for users both on and off Tencent Cloud and supports protection for website domain names and service ports.
- Access:
  - Anti-DDoS Pro is easy to access and you do not need to change your public IPs.
  - To access Anti-DDoS Advanced, you need to modify DNS or your application IPs.

## What are the differences between Anti-DDoS Pro and non-BGP protection?
|     Differences     | Anti-DDoS Pro             | Non-BGP Protection                  |
| -------- | -------------------- | ------------------- |
| Access costs | Low access costs without the need of changing your server IPs. | Complicated configuration where you need to replace your server IPs with non-BGP IPs and enter the domain name and port information. |
| Access quality | It uses BGP bandwidth and offers a lower access latency across networks and 30% higher access speed.         | It has no BGP bandwidth with a high network latency and poor quality.                              |
| Pricing policy | Billed according to the "number of protected IPs + protection times" with an all-out protection available at no additional elastic costs. | Billed in a complex manner with traffic fees incurred. |   

### What is hosted IP?
Hosted IP refers to a customized network routing solution, which is not provided by but can be protected by Anti-DDoS Pro.

If you need hosted IP, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### What will happen if the protection threshold of Anti-DDoS Pro is exceeded?
There is no concept of threshold in Anti-DDoS Pro.

### Does Anti-DDoS Pro Lightweight Edition allow three chances per month to manually unblock IPs?
Yes.

### Does Anti-DDoS Pro Lightweight Edition allow chances to manually unblock IPs for non-Lighthouse resources?
No.

### Which edition of Anti-DDoS Pro should I purchase if I use Lighthouse?
Both editions of Anti-DDoS Pro can be purchased to protect Lighthouse instances. The difference lies in the protection capabilities and discounts. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/36114).
