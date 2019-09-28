## Does Anti-DDoS Pro support non-Tencent Cloud IPs?
No. Anti-DDoS Pro only provides DDoS protection for public network IPs of Tencent Cloud. For protection of IPs other than Tencent Cloud, please [purchase Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/15483).

## What if the bound resource expires but the Anti-DDoS Pro instance does not expire? 
An Anti-DDoS Pro instance is purchased by month, and provides protection based on IPs. If the resource of the bound protected object expires and you do not replace the IP bound to the Anti-DDoS Pro instance, the instance may continue protection for the bound IP, but the corresponding resource may not be yours. You are advised to renew the cloud service in time or replace a new protected object IP.


## Does Anti-DDoS Pro protect domain names?
No. For domain name protection and application-layer protection, please [purchase Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/15483).

## The protection bandwidth of Anti-DDoS Basic is 2 Gbps. If I also purchase an Anti-DDoS Pro instance, will the final protection bandwidth be the sum of the two?
The final protection bandwidth a user enjoys is the protection bandwidth of the Anti-DDoS Pro instance. The default protection bandwidth of Anti-DDoS Basic will not add to it.
Assume the IP of a certain cloud virtual machine enjoys a 2 Gbps free protection bandwidth. Due to frequent attacks, the user purchases a 20 Gbps Anti-DDoS Pro instance for this IP, and then the maximum protection capability is 20 Gbps.

## What are the differences between Anti-DDoS Pro and Anti-DDoS Advanced?
- Protected objects:
 -  Anti-DDoS Pro only provides anti-DDoS protection for services within Tencent Cloud.
 -  Anti-DDoS Advanced is available for non-Tencent Cloud resources, providing non-Tencent Cloud service IPs/domain names with protection.
- Access:
  - The access configuration of Anti-DDoS Pro is more convenient without the need of changing public network IP addresses.
  - Anti-DDoS Advanced requires you to modify DNS or business IP before accessing the protection.

## What are the differences between Anti-DDoS Pro and non-BGP protection?
|     Differences     | Anti-DDoS Pro             | Non-BGP Protection                  |
| -------- | -------------------- | ------------------- |
| Cost of Access | It does not require changing of the server IP, and directly improves the defense capability of cloud products with immediate effect and low cost of access. | It requires you to replace the server IP with non-BGP IP and enter the domain name and port information. The configuration is quite complex. |
| Access Quality | It uses BGP bandwidths, minimizing access latency across networks. The access speed increases by over 30%.         | It has no BGP bandwidths, the network latency is higher, and the quality is poor.                              |
| Pricing Policy | The pricing policy is flexible. It allows for base + elastic pricing, and allows sharing.                              | The pricing policy is complex, and requires you to pay traffic fees.|

