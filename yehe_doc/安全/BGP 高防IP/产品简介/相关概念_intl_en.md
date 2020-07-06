## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of internet traffic.
### Network-Layer DDoS attack
A network-layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhaust its system-layer resources with a flood of internet traffic.
Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks.
### CC attack
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application-layer resources and exhausting its processing capacity.
Common attacks include HTTP/HTTPS-based GET/POST Flood, layer-4 CC, and Connection Flood attacks, etc.
<span id="fhfz"></span>
## Protection Bandwidth
This is divided into base protection bandwidth and elastic protection bandwidth.
- Base protection bandwidth: protection capability of an Anti-DDoS Advanced instance, which is prepaid on a monthly basis.
- Elastic protection bandwidth: maximum elastic protection capability of an Anti-DDoS Advanced instance, which is pay-as-you-go on a daily basis.

If elastic protection is not enabled, the maximum protection bandwidth of the Anti-DDoS Advanced instance will be the base protection bandwidth; otherwise, it will be the elastic protection bandwidth. If the attack traffic bandwidth exceeds the maximum protection bandwidth, blocking will be triggered.
>Elastic protection is disabled by default. If you need to use it, please check the pricing and billing information and enable it on your own. You can adjust the elastic protection bandwidth as needed at anytime.

### Elastic protection bandwidth usage
With elastic protection enabled, when the attack traffic bandwidth is higher than the base protection bandwidth but lower than the elastic protection bandwidth, Tencent Cloud Anti-DDoS Advanced will continue to protect your IPs to ensure the continuity of your business.

### Elastic protection billing
After elastic protection is enabled, it will be triggered and incur fees once the attack traffic bandwidth exceeds the base protection bandwidth. Fees will be charged based on the billing tier corresponding to the actual attack traffic peak on the day and a bill will be generated the next day.
For example, if you have purchased 20 Gbps base protection bandwidth and set the elastic protection bandwidth as 50 Gbps, when the actual attack bandwidth peak of the day is 35 Gbps, you need to pay for elastic protection at the price of the 30–40 Gbps tier.

## Cleansing
When the public network traffic of the target IP exceeds the threshold, Anti-DDoS will automatically cleanse the inbound traffic to the IP. The DDoS routing protocol will be used to redirect the traffic from the original network route to the DDoS cleansing devices of Anti-DDoS, which will identify the traffic, discard attack traffic, and forward normal traffic to the target IP.
In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly.
## Blocking
When the attack traffic suffered by the target IP exceeds the blocking threshold, Tencent Cloud will block all public network access requests to this IP through applicable ISP services to prevent other Tencent Cloud users from being affected. In short, when the bandwidth of the attack traffic suffered by your IP exceeds the maximum protection capability of your purchased Anti-DDoS Advanced instance, Tencent Cloud will block all public network access requests to it. When your IP is blocked, you can unblock it in the console in a self-service manner.

### Blocking threshold
The blocking threshold of an Anti-DDoS Advanced instance is the actual maximum protection bandwidth configured for the instance. Anti-DDoS Advanced provides different protection specifications. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/297/17435).
### Blocking duration
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
- Continuity of the attack: the blocking duration will extend if an attack continues. Once the period extends, a new blocking cycle will start.
- Frequency of the attack: users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking duration will extend automatically.
- Traffic volume of the attack: the blocking duration will extend automatically in case of ultra-large volume of attack traffic.

>For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold.

### Why is blocking necessary?
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked.
