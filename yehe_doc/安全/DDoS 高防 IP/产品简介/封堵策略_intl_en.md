## What is blocking?
Once the attack traffic exceeds the blocking threshold of the target IP, Tencent Cloud will block the IP from all public network access through ISP service to protect other Tencent Cloud users. In short, once the traffic attacking your IP goes over the maximum protection bandwidth you have purchased, Tencent Cloud will block the IP from all public network access. If your protected IP address is blocked, you can log in to [the console](https://console.cloud.tencent.com/ddos/antiddos-advanced/overview/ddos) to unblock it.

## Blocking Duration
An attacked IP is blocked for 2 hours by default. The actual duration can be up to 24 hours depending on how many times the IP is blocked and how high the peak attack bandwidth is.
The blocking duration is subject to the following factors:
- Continuity of the attack. The blocking period will extend if an attack continues. Once the period extends, a new blocking cycle will start.
- Frequency of the attack. Users that are frequently attacked are more likely to be attacked continuously. In such a case, the blocking period extends automatically.
- Traffic volume of the attack. The blocking period extends automatically in case of ultra-large volume of attack traffic.
>!For IPs that are blocked extra frequently, Tencent Cloud reserves the right to extend the duration and lower the threshold.

## Why can't my IP be unblocked immediately?
A DDoS attack usually does not stop immediately after the target IP is blocked and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis.

Since the IP blocking takes effect in the ISP's network, Tencent Cloud is unable to monitor whether or not the attack traffic flow has been stopped. If the IP is recovered while the attack is still going on, the IP will be blocked again, where there’s a gap between the recovery and the re-blocking that the attack traffic can take advantage of to directly enter the Tencent Cloud's classic network, resulting in negative effects on other cloud users. In addition, the IP blocking is a service Tencent cloud purchased from ISPs with limited numbers of blocking and blocking frequency.

## How to unblock my IP?
IP blocking is a service Tencent cloud purchased from ISPs with limited numbers of blocking and blocking frequency.
>?Only **three** chances of self-service unblocking are provided for Anti-DDoS Advanced users every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.

 For more details, see [Unblocking an IP](https://intl.cloud.tencent.com/document/product/297/43395).
