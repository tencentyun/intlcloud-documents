## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of internet traffic. 
### Network layer DDoS attack 
A network layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhausting its system layer resources with a flood of internet traffic. 

Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks. 
### CC attack 
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application layer resources and exhausting its processing capacity. 
Common attacks include HTTP/HTTPS-based GET/POST Flood, layer-4 CC, and Connection Flood attacks.

## Protection Capability
Protection capability refers to the ability to defend against DDoS attacks. The Anti-DDoS Pro service promises to provide max protection of no less than 30 Gbps subject to the maximum DDoS protection capability of Tencent Cloud in the current region.

## Cleansing
If the public network traffic of the target IP exceeds the preset protection threshold, Tencent Cloud Anti-DDoS service will automatically cleanse the inbound public network traffic of the target IP. With the Anti-DDoS routing protocol, the traffic will be redirected to the DDoS cleansing devices which will analyze the traffic, discard the attack traffic, and forward the clean traffic back to the target IP.

In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly. If no exception is found (which is dynamically determined based on the attack) in the traffic for a period of time, the cleansing system will determine that the attack has stopped and then stop cleansing.
  

## Blocking
Once the attack traffic exceeds the blocking threshold of the target IP, Tencent Cloud will block the IP from all public network access through ISP service to protect other Tencent Cloud users. In short, once the traffic attacking your IP goes over the maximum protection capacity of Tencent Cloud in the current region, Tencent Cloud will block the IP from all public network access. If your protected IP address is blocked, you can log in to the console to unblock it. 
### Blocking threshold 
The blocking threshold of a protected IP of an Anti-DDoS Pro instance is equal to the maximum protection capability in the current region. 
### Blocking duration 
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is. 
The blocking duration is subject to the following factors: 
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start. 
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically. 
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic. 

> ?For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold. 

### Why is blocking necessary? 
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked. 

