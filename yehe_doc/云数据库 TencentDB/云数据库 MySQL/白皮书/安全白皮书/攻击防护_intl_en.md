## DDoS Attack Prevention
When you use the public network to connect to and access a TencentDB for MySQL instance, you may suffer from DDoS attacks. To address this problem, Tencent Cloud provides traffic cleansing and blocking features that are automatically triggered and stopped by the system. When the Anti-DDoS system detects that your instance is under attacks, it will automatically enable traffic cleansing or block the traffic if the attacks cannot be resisted by cleansing or reach the blocking threshold.
>!You are recommended to access your TencentDB for MySQL instances over the private network to avoid DDoS attacks.

### Traffic cleansing
When the public network traffic of a TencentDB for MySQL instance exceeds the threshold, Anti-DDoS will automatically cleanse the inbound traffic to the instance. Policy-based routing will be used to redirect the traffic from the original network route to the DDoS cleansing devices of Anti-DDoS, which will identify the public network traffic, discard attack traffic, and forward normal traffic to the instance.

### Blocking
When the attack traffic suffered by a TencentDB for MySQL instance exceeds the blocking threshold, Tencent Cloud will block all public network access requests to this instance through applicable ISP services to prevent other Tencent Cloud users from being affected. This means that when the bandwidth of the attack traffic suffered by your instance exceeds the maximum protection bandwidth, Tencent Cloud will block all public network access requests to it.
- When the following conditions are met, blocking will be triggered:
 - The bits per second (bps) value reaches 2 Gbps.
 - Traffic cleansing is not effective.
- When the following condition is met, blocking will be stopped:
 - 2 hours elapses after blocking starts.
