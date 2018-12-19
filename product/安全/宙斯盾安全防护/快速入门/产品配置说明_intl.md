
Before purchasing a DDoS protective IP or protection pack, you need to confirm the following points:

## Preparations and Selection
- DDoS protective IP
DDoS protective IP uses proxy forwarding mode in which business traffic is pointed to the protective IP and then forwarded to the real server after being cleansed, achieving protection against DDoS attacks. Currently, DDoS protective IP can provide stable and secure protection against heavy-traffic DDoS attacks for Internet servers (including non-Tencent Cloud servers).
- DDoS protection pack
DDoS protection pack is a security product that directly provides protection capabilities for a range of cloud products such as CVM. Unlike DDoS protective IP, it directly binds cloud protection services to cloud products, so you don't need to have a forwarding IP or configure port-to-port forwarding rules.

## DDoS Protective IP
### Confirm the protective IP region and network
 - Region selection principle
DDoS protective IP work in proxy forwarding mode. Therefore, please try to select a region near the physical location of your real server. The closer the protective IP region is to the real server, the lower the access latency and the higher the access speed.
 - Network selection principle
When selecting the network, take into account the region and the needs for protection bandwidth. BGP network provides a better network experience, but its protection bandwidth is lower than that of non-BGP protective IPs. The protection bandwidth of non-BGP IPs decreases in sequence of China Telecom, China Unicom and China Mobile. Please select the corresponding ISP based on your end user distribution and try to avoid cross-ISP access.

### Confirm the configuration scheme for protective IP
 - Base protection bandwidth
 Prepaid. It is suggested that the base protection bandwidth be set to higher than the average historical attack traffic. This makes sure base protection is robust enough to prevent most attacks.
 - Elastic protection bandwidth
 Pay-per-use on a daily basis. It is suggested that the elastic protection bandwidth be set to higher than the highest historical attack traffic. This makes sure potential IP blocking is avoided in case of large-traffic attacks. Meanwhile, elastic protection is billed on a monthly basis and you only pay for what you use, significantly reducing the costs.
 - Forwarded business traffic
 This is the non-attacking traffic of normal business requests forwarded to the real server. It can be charged by bandwidth or by traffic. It is recommended to select based on the characteristics of normal business traffic.

## DDoS Protection Pack
### Principle for Protection Pack Region Selection
 - Region selection principle
	DDoS protection pack can only provide protection for Tencent Cloud public IPs in the same region where it is available. Therefore, please be sure to select the pack available in the region where your Tencent Cloud real server is located.
	
### Confirm the configuration scheme for protection pack
- Protection scope
You can choose single-IP or multi-IP mode. In single-IP mode, the protection pack can be bound to one Tencent Cloud public IP which utilizes the protection bandwidth exclusively. In multi-IP mode, the protection pack can be bound to multiple Tencent Cloud public IPs which share the resources. When multiple IPs are under DDoS attacks, if the bandwidth of the combined attack traffic is higher than the protection bandwidth, blocking will start from the IP address suffering the largest attack traffic.
- Base protection bandwidth
 Prepaid. It is suggested that the base protection bandwidth be set to higher than the average historical attack traffic. This makes sure base protection is robust enough to prevent most attacks.
- Elastic protection bandwidth
Pay-per-use on a daily basis. It is suggested that the elastic protection bandwidth be set to higher than the highest historical attack traffic. This makes sure potential IP blocking is avoided in case of large-traffic attacks. Meanwhile, elastic protection is billed on a monthly basis and you only pay for what you use, significantly reducing the costs.
- Elastic billing method
Elastic protection supports two billing methods: elastic traffic pack and elastic bandwidth. An elastic traffic pack needs to be purchased in advance. If the attack exceeds the base protection bandwidth and elastic protection traffic is consumed, the usage amount will be deducted from the pack accordingly. Compared with the elastic bandwidth method, elastic protection packs can significantly reduce your costs of elastic protection in scenarios with low-frequency, high-bandwidth short attacks If your business is attacked frequently and the attack lasts for a prolonged time, you can choose to be billed by the elastic bandwidth which is pay-per-use on a daily basis.
- Elastic traffic pack
If "elastic traffic pack" is selected as the billing method for elastic protection and elastic protection is triggered, the incurred elastic traffic will be deducted from a purchased elastic traffic pack in the same region. If no pack has been purchased or the purchased pack is used up, the elastic protection capability will be suspended.
- Elastic protection bandwidth
If "elastic protection bandwidth" is selected as the billing method for elastic protection and elastic protection is triggered, you will be billed by the elastic protection bandwidth on a daily basis.

