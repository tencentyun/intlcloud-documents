AIA can optimize IP transmission quality and enable multi-entry nearby access. This document describes the application scenarios of AIA.
## Game Acceleration
An Anycast IP can be used for gaming acceleration. Through AIA, game requests can access Tencent Cloud from nearby entries and get to game servers through Tencent Cloud's private network, greatly shortening the public network path and reducing problems such as latency, network jitter, and packet loss. Compared with the traditional acceleration service, an Anycast IP requires no extra deployment of traffic receivers at the entry and eliminates the need for zoning, thus simplifying DNS deployment.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/i2ne440_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


## Interactive Live Video Broadcasting (ILVB)
If high-quality and latency-free audio/video streaming is desired during live video broadcasting (LVB) in the case of cross-region transmission, the LVB platform needs to establish the dedicated network and access points that cover multiple regions. With the aid of AIA, the LVB platform can directly use Tencent Cloud's private network and POPs to serve users, without the need to set up a dedicated network connection from scratch.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/E7I3409_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-2.png)

## Financial Service
Financial services such as securities trading highly require real-time performance, but unstable public network transmission cannot meet this requirement. After the access layer of financial applications is bound to an Anycast IP, data can be transmitted over Tencent Cloud's private network to make these applications available in multiple regions. In addition, the AIA service also allows the same IP to be used in multiple regions, which simplifies IP-related approval work, such as ICP filing and registration with financial regulator registration.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/983d465_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.svg)

## Security Service
Security cleansing service providers, games, and large website applications are often under various high-traffic attacks such as Syn Flood and ICMP Flood. An ordinary public IP is generally published in a single region, so all attack traffic flows through the single ingress/egress. With AIA, an IP can be simultaneously published in multiple regions without the need to change the DNS configuration, and the attack traffic is diverted to nearby ingresses for processing.
>Anti-DDoS Basic is enabled for AIA by default, which gives an AIA IP the same basic DDoS attack prevention capabilities enjoyed by a BGP IP. If you need a higher level of protection, please purchase [Anti-DDoS Pro](https://www.tencentcloud.com/document/product/1029).
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RsuE490_PRELIM__Anycast%20%E5%85%AC%E7%BD%91%E5%8A%A0%E9%80%9F_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-4.svg)

