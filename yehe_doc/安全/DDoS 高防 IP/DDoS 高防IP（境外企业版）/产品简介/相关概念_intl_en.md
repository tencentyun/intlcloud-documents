## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of internet traffic.

### Network layer DDoS attack
A network layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhausting its system layer resources with a flood of internet traffic.

Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks.

### CC attack
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application layer resources and exhausting its processing capacity. Common attacks include HTTP/HTTPS-based GET/POST Flood, layer-4 CC, and Connection Flood attacks.

## Protection Capability
Protection capability refers to the capability to defend against DDoS attacks. Anti-DDoS Advanced (Global Enterprise Edition) intelligently schedules global node resources for max protection.

## Anycast 
The protection address (Anycast EIP) is broadcast to ISPs in various regions through BGP Anycast. After this IP is bound with backend resources, user traffic (including normal traffic and attack traffic) in the access regions will be directed to the nearest Tencent Cloud node (Anycast access point) for near-source cleansing. Smart routing and automatic network scheduling are used together to stably deliver users' network access requests to the instances in Tencent Cloud.

## Cleansing
If the public network traffic of the target IP exceeds the preset protection threshold, Tencent Cloud Anti-DDoS service will automatically cleanse the inbound public network traffic of the target IP. With the Anti-DDoS routing protocol, the traffic will be redirected to the DDoS cleansing devices which will analyze the traffic, discard the attack traffic, and forward the clean traffic back to the target IP.

In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly. If no exception is found (which is dynamically determined based on the attack) in the traffic for a period of time, the cleansing system will determine that the attack has stopped and then stop cleansing.

## Blocking
Once the attack traffic exceeds the blocking threshold of the target IP, Tencent Cloud will block the IP from all public network access through ISP service to protect other Tencent Cloud users. In short, once the traffic attacking your IP goes over the maximum protection capacity of Tencent Cloud in the current region, Tencent Cloud will block the IP from all public network access. If your protected IP address is blocked, you can log in to the console to unblock it.

### Blocking duration
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
•	Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start.
•	Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically.
•	Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic.

### Blocking level	
- Single-ISP: one single ISP is blocked. In this case, the application cannot be accessed in one or more regions through this ISP.
- Single-Region nodes: nodes in one single region are blocked. In this case, the application cannot be accessed in this region.
- All regions: Tencent Cloud directly blocks access to the application. In this case, the application cannot be accessed globally.

>?
>- According to the extent of the impact surface of attacks, different levels of blocking will be triggered.
>- For example, after a customer suffers DDoS attacks, when the attack traffic reaches the blocking threshold of the ISP, the ISP will be blocked; when the attack traffic reaches the node blocking threshold of a region, nodes in the region will be blocked, and the customer's application will be inaccessible in the region; when the total attack traffic suffered by the customer on all nodes reaches the all-region blocking threshold, the customer's application will be blocked in all regions, and it will be inaccessible globally.

### Scheduling
When the traffic reaches the threshold of the current ISP, cross-ISP scheduling will be performed to ensure the application availability.
>? To ensure the application availability, several rounds of scheduling may occur.
