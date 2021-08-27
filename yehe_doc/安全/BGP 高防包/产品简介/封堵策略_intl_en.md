## What is blocking?
Once the attack traffic exceeds the blocking threshold of a target IP, Tencent Cloud will block the target IP from all public network accessing through ISP service to protect other Tencent Cloud users.
>?The blocking threshold of a protected IP of an Anti-DDoS Pro instance is equal to the maximum protection capability in the current region.
>- New Anti-DDoS Pro will provides all-out protection capability of at least 30 Gbps.
>- Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack.
>- The maximum protection bandwidth is 300 Gbps for Guangzhou, 250 Gbps for Beijing, and 500 Gbps for Shanghai, which will be dynamically adjusted based on the actual network status.

In short, once the traffic attacking your IP goes over the maximum protection bandwidth Tencent Cloud provided, Tencent Cloud will block the IP from all public networks’ access.

## How to unblock my IP?
IP blocking is a service Tencent cloud purchased from ISPs with limited numbers of blocking and blocking frequency.
>?Only **three** chances of self-service unblocking are provided for Anti-DDoS Pro users every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.

If you do not want to wait until the IP is unblocked automatically, see [An application was blocked due to high-traffic attacks](https://intl.cloud.tencent.com/document/product/1029/40511).

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

## Why can't my IP be unblocked immediately?
A DDoS attack usually does not stop immediately after the target IP is blocked and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis.

Since the IP blocking takes effect in the ISP's network, Tencent Cloud is unable to monitor whether or not the attack traffic flow has been stopped. If the IP is recovered while the attack is still going on, the IP will be blocked again, where there’s a gap between the recovery and the re-blocking that the attack traffic can take advantage of to directly enter the Tencent Cloud's classic network, resulting in negative effects on other cloud users. In addition, the IP blocking is a service Tencent cloud purchased from ISPs with limited numbers of blocking and blocking frequency.
