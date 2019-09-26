## DDoS Attacks
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make service unavailable by blocking the network bandwidth or overwhelming the system of the target server with a flood of Internet traffic. 
### Network Layer DDoS Attacks 
A network layer DDoS attack attempts to make service unavailable by blocking the network bandwidth to exhaust system layer resources of the target server using a flood of Internet traffic. 
Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/memcached attacks. 
### CC Attacks 
A CC attack is a malicious attempt to make service unavailable by occupying application layer resources and exhausting the processing performance of the target server. 
Common attacks include GET/POST Flood, Layer-4 CC, and Connection Flood based on HTTP/HTTPS.
<span id="fhfz"></span>
## Protection Bandwidth
The protection bandwidth consists of the base protection bandwidth and elastic protection bandwidth. 
- Base protection bandwidth: Monthly prepaid Anti-DDoS service plan that provides base bandwidth protection of an Anti-DDoS Pro instance. 
- Elastic protection bandwidth: The max possible protection bandwidth of the instance. The elastic protection bandwidth is billed on a postpaid daily basis. 

If the elastic protection is disabled, the base protection bandwidth is the maximum bandwidth of the Anti-DDoS Pro instance. If elastic protection is enabled, the elastic protection bandwidth is the maximum bandwidth of the Anti-DDoS Pro instance. IP blocking is triggered when traffic exceeds the maximum protection bandwidth of the Anti-DDoS Pro instance. 
>Elastic protection is disabled by default. Enable elastic protection after checking the related costs of this service. You can adjust the elastic protection bandwidth as required. 
### Function of the Elastic Protection Bandwidth 
After elastic protection is enabled, if the traffic peak exceeds the purchased base protection bandwidth and remains within the elastic protection bandwidth, Tencent Cloud Anti-DDoS Pro continues protection to ensure business continuity. 
### Elastic Protection Fees 
After elastic protection is enabled, the elastic protection will be triggered if the traffic exceeds the base protection bandwidth, and will incur cost according to the billing tier of the peak attack bandwidth. The related bill is generated on the following day. 
For example, assume that you have purchased 20 Gbps of base protection bandwidth and set the elastic protection bandwidth as 50 Gbps. If the actual peak attack bandwidth of the day is 35 Gbps, then you need to pay elastic protection fees according to the tier of 30-40 Gbps. 
For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747). 
## Cleansing
If the public network traffic of the target IP exceeds the set protection threshold, Tencent Cloud Anti-DDoS service will automatically cleanse the inbound public network traffic of the target IP. The BGP routing protocol redirects the traffic of the original network path to the DDoS cleansing devices of the Anti-DDoS service. The cleansing devices identify the traffic of the IP, discard the attack traffic, then forward the clean traffic to the target IP. 
In general, cleansing does not influence regular access, except for special occasions or when the cleansing policy is incorrectly configured. 
## Blocking
When the attack traffic exceeds the blocking threshold of the target IP, Tencent Cloud will shield access from external networks through services of the carrier to protect other users on the cloud platform. In short, when one of your IPs is attacked by Internet traffic which exceeds the maximum [protection bandwidth](#fhfz) you have purchased, Tencent Cloud will shield access from external networks to the attacked IP. When your protection IP is blocked, you can log in to the console for [self-unblocking](https://intl.cloud.tencent.com/document/product/1029/31758). 
### Threshold 
The blocking threshold of the protection IP of the Anti-DDoS Pro instance is the maximum [protection bandwidth](#fhfz) that you have purchased. The Anti-DDoS Pro provides multiple packs. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747). 
### Duration 
The blocking period is 2 hours by default. The actual duration can be up to 24 hours, depending on the triggering times and peak attack bandwidth. 
The duration of the blocking period is influenced by the following elements: 
- Continuity. The blocking period extends when an attack continues. The duration of this period is calculated when the extension takes place. 
- Frequency. Users that are frequently attacked are more likely to be attacked continuously. In these cases, the blocking period extends automatically. 
- Traffic volume. The blocking period extends automatically to offer protection against ultra-large attack traffic volumes. 

>For users with frequent blocks, Tencent Cloud reserves the right to extend the duration and reduce the threshold. 

### Reasons for Blocking 
Tencent Cloud reduces the cost by sharing the infrastructure, with one public IP being shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, in addition to the target servers. To protect other servers and to ensure the network stability, we need to block the target server IP. 

### Reasons for Charging for Anti-DDoS Service 
DDoS attacks have negative effects on not only the targets but also the entire cloud network, affecting other non-attacked users in Tencent Cloud as well. Moreover, building the anti-DDoS system costs high, including the cleansing cost and the bandwidth cost. Specifically, the largest expense is bandwidth and it is calculated based on the total traffic. No difference exists between normal traffic and attack traffic in terms of the bandwidth cost.  
Therefore, although Tencent Cloud can afford limited free DDoS Basic service for all users, we have to block inbound public network traffic of the attacked servers when the attack traffic exceeds the free quota.
For more information, please see [Block FAQs](https://intl.cloud.tencent.com/document/product/1029/31772).