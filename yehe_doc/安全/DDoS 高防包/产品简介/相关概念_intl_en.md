## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of internet traffic. 

### Network-layer DDoS attack 
A network-layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhaust its system-layer resources with a flood of internet traffic. 

Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks. 

## Protection Capability
Protection capability refers to the ability to defend against DDoS attacks. The Anti-DDoS Pro service promises an all-out protection with Tencent Cloud's maximum DDoS protection capability in the current region.

## Cleansing
When the public network traffic of the target IP exceeds the threshold, Anti-DDoS will automatically cleanse the inbound traffic to the IP. The DDoS routing protocol will be used to redirect the traffic from the original network route to the DDoS cleansing devices of Anti-DDoS, which will identify the traffic, discard attack traffic, and forward normal traffic to the target IP. 
In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly. 

## Blocking
When the attack traffic suffered by the target IP exceeds the blocking threshold, Tencent Cloud will block all public network access requests to this IP through applicable ISP services to prevent other Tencent Cloud users from being affected. In short, when the bandwidth of the attack traffic suffered by your IP exceeds the maximum protection capability of Tencent Cloud in the current region, Tencent Cloud will block all public network access requests to it. When your IP is blocked, you can unblock it in the console in a self-service manner. 
### Blocking threshold 
The blocking threshold of a protected IP of an Anti-DDoS Pro instance is equal to the maximum protection capability in the current region. 
### Blocking duration 
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is. 
The blocking duration is subject to the following factors: 
- Continuity of the attack: the blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start. 
- Frequency of the attack: users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically. 
- Traffic volume of the attack: the blocking period extends automatically in case of ultra-large volume of attack traffic. 

>For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold. 

### Why is blocking necessary? 
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked. 

