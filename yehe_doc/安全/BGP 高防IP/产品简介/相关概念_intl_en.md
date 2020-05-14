## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or exhausting its system resources with a flood of attacking requests sent from large numbers of botnets.
### Network-Layer DDoS Attack
A network-layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhausting its system-layer resources with a flood of internet traffic.
Common attacks include SYN flood, ACK flood, UDP flood, ICMP flood, and DNS/NTP/SSDP/Memcached reflection attacks.
### CC Attack
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application-layer resources and exhausting its processing capacity.
Common attacks include HTTP/HTTPS-based GET/POST flood, layer-4 CC, and connection flood attacks, etc.
<span id="fhfz"></span>
## Protection Bandwidth
There are two types of protection bandwidth: base protection bandwidth and elastic protection bandwidth.
- Base protection bandwidth: base protection bandwidth of the Anti-DDoS service instance.
- Elastic protection bandwidth: the largest possible protection bandwidth of the Anti-DDoS service instance. The part in excess of the base protection bandwidth is billed daily in a pay-as-you-go manner.

If elastic protection is not enabled, the maximum bandwidth of an Anti-DDoS service instance will be the base protection bandwidth. If elastic protection is enabled, the maximum bandwidth will be the elastic protection bandwidth. Once the attack traffic exceeds the maximum protection bandwidth, IP blocking will be triggered.
>Elastic protection is disabled by default. If you need the feature, please check the pricing and billing information and enable it on your own. You can adjust the elastic protection bandwidth as required.

### Benefits of Elastic Protection Bandwidth
With elastic protection enabled, when the attack traffic is higher than the base protection bandwidth but lower than the elastic protection bandwidth, Tencent Cloud Anti-DDoS Advanced will continue to protect your IPs to ensure your business continuity.
### Elastic Protection Billing
With elastic protection enabled, elastic protection will be triggered and incur fees once the attack traffic goes over the base protection bandwidth. You will be billed on the following day based on the peak attack bandwidth of the current day.
For example, assume that you have purchased 20 Gbps of base protection bandwidth and set the elastic protection bandwidth as 50 Gbps. If the actual peak attack bandwidth of the day is 35 Gbps, you will need to pay for the elastic protection at the price of the 30–40 Gbps tier.
For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/297/17435).
## Cleansing
When the public network traffic of a target IP exceeds the threshold, Anti-DDoS will automatically cleanse the inbound traffic to the IP. The BGP routing protocol will be used to redirect the traffic from the original network route to the DDoS cleansing devices of Anti-DDoS, which will identify the traffic, discard attack traffic, and forward normal traffic to the IP.
In general, cleansing does not affect normal access except on special occasions or when the cleansing policy is configured improperly.
## Blocking
When the attack traffic suffered by a target IP exceeds the blocking threshold, Tencent Cloud will block all public network access requests to this IP through applicable ISP services to protect other Tencent Cloud users from being affected. This means that when the bandwidth of the attack traffic suffered by your IP exceeds the [maximum protection bandwidth](#fhfz) of your purchased Anti-DDoS package, Tencent Cloud will block all public network access requests to it. If your protected IP is blocked, you can log in to the console to [unblock it](https://intl.cloud.tencent.com/document/product/297/34090).
Block
### Blocking threshold
The blocking threshold of a protected IP equals the maximum [protection bandwidth](#fhfz) you have purchased. Anti-DDoS Advanced offers various specifications. For more information, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/297/17435).
### Blocking period
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start.
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically.
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic.

>For IPs that are blocked too frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold.

### Why is my IP blocked?
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked.
### Why isn't anti-DDoS service always free?
DDoS attacks threaten not only the targets but also the entire cloud network and affect non-attacked Tencent Cloud users as well. In addition, DDoS protection incurs high costs, including cleansing fees and bandwidth fees, among which bandwidth costs the most. Bandwidth fees are calculated based on the total amount of traffic, and there is no difference between fees incurred by normal traffic and attack traffic.
Therefore, Tencent Cloud provides Anti-DDoS Basic service free of charge for all users. However, once the attack traffic exceeds the free protection threshold, we will have to block the attacked IP from all public network access.
For more information on blocking, please see [Blocking](https://intl.cloud.tencent.com/document/product/297/16608).
