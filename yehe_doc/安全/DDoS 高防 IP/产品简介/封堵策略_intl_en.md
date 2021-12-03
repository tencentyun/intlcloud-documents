## What is blocking?
Once the attack traffic exceeds the blocking threshold of a target IP, Tencent Cloud will block the target IP from all public network accessing through ISP service to protect other Tencent Cloud users.
>?
>The blocking threshold of a protected IP of an Anti-DDoS Advanced instance is equal to the maximum protection capability in the current region.
>- New Anti-DDoS Advanced will provides all-out protection capability of at least 30 Gbps.
>- Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack.
>- The maximum protection bandwidth is 300 Gbps for Guangzhou, 250 Gbps for Beijing, and 500 Gbps for Shanghai, which will be dynamically adjusted based on the actual network status.

In short, once the traffic attacking your IP goes over the maximum protection bandwidth Tencent Cloud provided, Tencent Cloud will block the IP from all public networks’ access.


## How to unblock my IP?
IP blocking is a service Tencent cloud purchased from ISPs with limited numbers of blocking and blocking frequency.
>?Only **three** chances of self-service unblocking are provided for Anti-DDoS Advanced users every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.


## Why is my IP blocked?
Tencent Cloud reduces cloud costs by sharing infrastructure, with one public IP shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, not only the attack targets.

To protect other users and ensure network stability, we have to block the target IP.

## Blocking Duration
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start.
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically.
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic.
>?For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold.



