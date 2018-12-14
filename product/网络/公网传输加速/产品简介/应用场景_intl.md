Tencent Cloud Anycast public network acceleration can achieve IP transmission quality optimization and multi-entry access, the following will introduce you to its application scenarios.
## **Gaming Acceleration**
An Anycast IP can serve as a gaming accelerator. A gaming request enters Tencent Cloud through the nearest node and then reaches the game server through Tencent Cloud's private Direct Connect line, significantly shortening the Internet path distance and reduces latency, jitter and packet loss. Compared with traditional acceleration services, AIA simplifies DNS deployment as IP entries do not require deployment of additional traffic receiving devices and IPs do not need to be geographically differentiated.

![p](https://main.qcloudimg.com/raw/08d2e4255c3c93c89535fa2504eecf61.svg)

## **Live Video Interaction**
Clear video and voice have to be relayed without delay during cross-region transfer of live streaming content, meaning the live streaming platform must build a dedicated network and access points covering multiple regions. With the help of AIA, the platform can directly utilize Tencent Cloud's backbone networks and POPs to serve live streaming users without the need to set up a dedicated network.

![Scenario 2](https://main.qcloudimg.com/raw/32fd41164655da00749b9b5f97bc29cf.svg)

## **Financial Services**
Financial services such as securities require high real-time performance, making unstable Internet transfers completely unsatisfactory. The access layer of an application in this field can be bound to an Anycast IP for multi-region coverage, made possible by private network transfer on Tencent Cloud's backbone networks. Further, AIA enables the use of the same IP for multiple regions, simplifying the paperwork for IP-related approvals such as ICP license filing and registration with financial regulatory authorities.

![Scenario 3](https://main.qcloudimg.com/raw/76748d6e22b0e43d87418cf264c7e169.svg)

## **Security Services**
Security cleansing service providers, gaming platforms and large-scale website applications are often faced with various traffic-based attacks such as SYN floods and ICMP floods. A common public IP is published in one single region, so all the attacking traffic is concentrated in the same entry. With AIA, the IP is published simultaneously in multiple regions, and the attacking traffic can be diverted to multiple entries for absorption without the need to modify the DNS configuration.

![Scenario 4](https://main.qcloudimg.com/raw/d2cf61f3cf70307dc736988be76c067e.svg)
