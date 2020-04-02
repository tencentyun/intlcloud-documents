## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of Internet traffic. 
### Network Layer DDoS Attack 
A network layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhaust its system layer resources with a flood of Internet traffic. 
Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks. 
### CC Attack 
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application layer resources and exhausting its processing capacity. 
Common attacks include HTTP/HTTPS-based GET/POST Flood, Layer-4 CC, and Connection Flood attacks, etc.
<span id="fhfz"></span>
## Protection Bandwidth
There are two types of protection bandwidth: base protection bandwidth and elastic protection bandwidth. 
- Base protection bandwidth: base protection bandwidth of the Anti-DDoS Pro instance. 
- Elastic protection bandwidth: the largest possible protection bandwidth of the Anti-DDoS Pro instance. The part that exceeds the base protection bandwidth is billed per day according. 

If elastic protection is not enabled, the maximum bandwidth of an Anti-DDoS Pro instance will be the base protection bandwidth. If elastic protection is enabled, the maximum bandwidth will be the elastic protection bandwidth. Once the attack traffic exceeds the maximum protection bandwidth, IP blocking will be triggered. 
>Elastic protection is disabled by default. If you need the feature, please check the pricing and billing information and enable it yourself. You can adjust the elastic protection bandwidth as required. 
### Benefits of Elastic Protection Bandwidth 
With elastic protection enabled, when the attack traffic is higher than the base protection bandwidth but lower than the elastic protection bandwidth, Tencent Cloud Anti-DDoS Pro will continue to protect your IPs to ensure the continuity of your business. 
### Elastic Protection Billing 
With elastic protection enabled, elastic protection will be triggered and incur fees once the attack traffic goes over the base protection bandwidth. You will be billed on the following day based on the peak attack bandwidth of the current day. 
For example, assume that you have purchased 20 Gbps of base protection bandwidth and set the elastic protection bandwidth as 50 Gbps. If the actual peak attack bandwidth of the day is 35 Gbps, you will need to pay for the elastic protection according to the price of the 30-40 Gbps tier. 
For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747). 
## Cleansing
If the public network traffic of the target IP exceeds the pre-set protection threshold, Tencent Cloud Anti-DDoS service will automatically cleanse the inbound public network traffic of the target IP. With the BGP routing protocol, the traffic will be redirected to the DDoS cleansing devices which will analyze the traffic, discard the attack traffic, and forward the clean traffic back to the target IP. 
In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly. 
## Blocking
Once the attack traffic exceeds the blocking threshold of the target IP, Tencent Cloud will block the IP from all public network access through ISP service to protect other Tencent Cloud users. In short, once the traffic attacking your IP goes over the maximum [protection bandwidth](#fhfz) you have purchased, Tencent Cloud will block the IP from all public network access. If your IP address is blocked, you can log in to the console to [unblock it](https://intl.cloud.tencent.com/document/product/1029/31758). 
### Blocking Threshold 
The blocking threshold of a protected IP equals the maximum [protection bandwidth](#fhfz) you have purchased. Anti-DDoS Pro offers various options. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1029/31747). 
### Blocking Duration 
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is. 
The blocking duration is subject to the following factors: 
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start. 
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically. 
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic. 

>For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold. 

### Why is blocking necessary 
Tencent Cloud reduces costs of using clouds by sharing the infrastructure, with one public IP shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, we have to block the target server IP. 

### Why isn’t anti-DDoS service always free 
DDoS attacks not only threaten the targets but also the entire cloud network, affecting non-attacked Tencent Cloud users as well. Also, DDoS protection incurs high costs, including cleansing costs and bandwidth costs, in which bandwidth costs the most. Bandwidth costs are calculated based on the total amount of traffic; there is no difference between costs incurred by normal traffic and attack traffic. 
Therefore, Tencent Cloud provides Anti-DDoS Basic service free of charge for all users. But once the attack traffic exceeds the free quota, we will have to block the attacked IP from all public network access.
For more information on IP blocking, see [About Blocking](https://intl.cloud.tencent.com/document/product/1029/31772).
