Tencent Cloud Anycast Internet Acceleration (AIA) can implement quality optimization of IP transfer and nearby access to network through multiple entries. This document describes the application scenarios of AIA.
## Gaming Acceleration
An Anycast IP can be used for gaming acceleration. Through AIA, game requests can have nearby access to Tencent Cloud and get to game servers through Tencent Cloud's private network, greatly shortening the public network path and reducing problems such as delay, jitter, and packet loss. Compared to the traditional acceleration, an Anycast IP requires no extra deployment of traffic receivers at the entry and eliminates the need for zoning, thus simplifying DNS deployment.
![](https://main.qcloudimg.com/raw/d482c6f14176ad6b67f5a1aafaa97641.png)

## Interactive Live Video Broadcasting (ILVB)
If high-quality and delay-free audio/video streaming is desired during live video broadcasting (LVB) in the case of cross-region transfer, the dedicated network connection and access points covering multiple regions are required for the LVB platform. With the aid of AIA, the LVB platform can directly use Tencent Cloud's private network and POPs to serve users, eliminating the need to build a dedicated network connection from scratch.
![](https://main.qcloudimg.com/raw/db1ca84c4ae97b2365a1a3daa7b61b0d.png)

## Financial Service
Financial services such as securities trading require very high real-time performance, and unstable public network transfer obviously cannot meet this requirement. After the access layer of financial applications is bound to an Anycast IP, data can be transferred over Tencent Cloud's private network to make these applications available in multiple regions. In addition, the AIA service also allows the same IP to be used in multiple regions, which simplifies IP-related approval work, such as application for ICP filing and registration with financial regulators.
![Scenario 3](https://main.qcloudimg.com/raw/dde74492ff3b59a9425262b76aba6c49.png)

## Security Service
Security cleansing service providers, games, and large website applications are often under various high-traffic attacks such as SYN floods and ICMP floods. An ordinary public IP is generally published in a single region; therefore, all attack traffic flows through the single ingress/egress. After AIA is used, an IP can be simultaneously published in multiple regions without the need to change the DNS configuration, and attack traffic is diverted to different ingresses for processing.
>Anti-DDoS Basic is enabled for AIA by default, which gives an AIA IP the same basic DDoS attack prevention capabilities enjoyed by a BGP IP. If you need a higher level of protection, please purchase [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029).
>
![Scenario 4](https://main.qcloudimg.com/raw/2ce84f64426a115472d6cb9ec5464e91.png)
