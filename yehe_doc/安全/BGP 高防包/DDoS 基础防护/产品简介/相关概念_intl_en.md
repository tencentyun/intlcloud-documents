## DDoS Attack
A Distributed Denial of Service (DDoS) attack is a malicious attempt to make a targeted server unavailable by blocking its network bandwidth or overwhelming its system with a flood of Internet traffic.

### Network layer DDoS attack
A network layer DDoS attack attempts to make a targeted server unavailable to its intended users by blocking its network bandwidth and exhausting its system layer resources with a flood of Internet traffic.
Common attacks include SYN Flood, ACK Flood, UDP Flood, ICMP Flood, and DNS/NTP/SSDP/Memcached reflection attacks.

### CC attack
A CC attack is a malicious attempt to make a targeted server unavailable by occupying its application layer resources and exhausting its processing capacity.
Common attacks include HTTP/HTTPS-based GET/POST Flood, layer-4 CC, and connection flood attacks, etc.

## Cleansing
If the public network traffic of the target IP exceeds the pre-set protection threshold, Tencent Cloud Anti-DDoS service will automatically cleanse the inbound public network traffic of the target IP. With the Anti-DDoS routing protocol, the traffic will be redirected to the DDoS cleansing devices which will analyze the traffic, discard the attack traffic, and forward the clean traffic back to the target IP.
In general, cleansing does not affect access except on special occasions or when the cleansing policy is configured improperly. If no exception is found (which is dynamically determined based on the attack) in the traffic for a period of time, the cleansing system will determine that the attack has stopped and then stop cleansing.

## Blocking
### Blocking threshold
The default blocking threshold of Anti-DDoS Basic:

| Region | General User | VIP User |
|---------|---------|---------|
| Chinese mainland | 2 Gbps | 10 Gbps |
|Outside the Chinese mainland|2 Gbps |2 Gbps|

### Blocking duration
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start.
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically.
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volumes of attack traffic.

>!For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold.

### Why is blocking necessary
Tencent Cloud reduces costs of using clouds by sharing the infrastructure, with one public IP shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, we have to block the target server IP.

### Why isn't anti-DDoS service always free
DDoS attacks not only threaten the targets but also the entire cloud network, affecting non-attacked Tencent Cloud users as well. Also, DDoS protection incurs high costs, including cleansing costs and bandwidth costs, in which bandwidth costs the most. Bandwidth costs are calculated based on the total amount of traffic; there is no difference between costs incurred by normal traffic and attack traffic.
Therefore, Tencent Cloud provides Anti-DDoS Basic service free of charge for all users. But once the attack traffic exceeds the free quota, we will have to block the attacked IP from all public network access.
