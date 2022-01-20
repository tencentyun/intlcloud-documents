This document describes the strengths of CLB.

## High Performance
One single CLB cluster (not one instance) can support hundreds of millions of concurrent connections and process millions of data packets per second. This enables you to easily sustain ecommerce websites, social networking platforms, and gaming businesses with over 10 million daily page views.

## High Availability
CLB adopts a cluster-based deployment mode to deliver an availability up to 99.95%. In the extreme case where only one CLB instance is available, it can still support tens of millions of concurrent connections. The cluster system will remove faulty instances in time and keep the healthy ones to ensure that the real server continues to operate properly.

## High Elasticity
The CLB cluster scales the service capabilities of the application system elastically according to the business load, and automatically creates and releases CVM instances through the dynamic scaling group of Auto Scaling. These features, in conjunction with a dynamic monitoring system and a billing system that is accurate to the second, eliminate your need to manually intervene or estimate resource requirements, helping you reasonably allocate computing resources and prevent resource waste.

## High Security and Stability
With the aid of BGP Anti-DDoS system, CLB is capable of defending against most network attacks (such as DDoS, CC, and web intrusion attacks) and cleansing attacking traffic in a matter of seconds, which greatly avoids the occurrence of blocked IPs and full occupancy of bandwidth. Its built-in synproxy anti-attack mechanism prevents the backend CVM instances from being crashed by attacks before the Anti-DDoS system takes effect, which makes data more secure and stable.
CLB strictly isolates the traffic of each tenant and provides active protection against DDoS attacks. Public network CLB supports [Anti-DDoS Basic](https://intl.cloud.tencent.com/document/product/1029/41715) by default. Moreover, CLB further supports [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029), [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297), [WAF](https://intl.cloud.tencent.com/document/product/627), and other security products to safeguard your businesses.

>? 
> - If you have higher protection requirements, you can purchase [Anti-DDoS Pro](https://intl.cloud.tencent.com/product/ddos-bgp). It provides a DDoS protection capability of at least 30 Gbps, and the maximum protection capability is dynamically adjusted according to the actual network conditions in each region.
> - To protect the application layer, you can purchase [WAF](https://intl.cloud.tencent.com/product/waf). It protects web security at the application layer against web vulnerability attacks, malicious crawlers, and CC attacks. 
> 

## Low Costs
CLB eliminates your need to invest in additional load balancing hardware and time devoted to tedious OPS work, saving you up to 99% of hardware and labor costs. It supports multiple billing modes for your choice as needed.


