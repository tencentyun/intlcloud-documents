### Why is my IP blocked?
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked.

### Why isn't anti-DDoS service always free?
DDoS attacks threaten not only the targets but also the entire cloud network and affect non-attacked Tencent Cloud users as well. In addition, DDoS protection incurs high costs, including cleansing fees and bandwidth fees, among which bandwidth costs the most. Bandwidth fees are calculated based on the total amount of traffic, and there is no difference between fees incurred by normal traffic and attack traffic.
Therefore, Tencent Cloud provides Anti-DDoS Basic service free of charge for all users. However, once the attack traffic exceeds the free protection threshold, we will have to block the attacked IP from all public network access.

### Why can't my IP be unblocked immediately?
A DDoS attack usually does not stop immediately after the target IP is blocked and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis.
Since IP blocking takes effect in ISP network, Tencent Cloud cannot monitor whether the attack traffic has stopped after the attacked public IP is blocked. If the IP is unblocked but the attack is still going on, the IP will be blocked again. During the gap between the IP being unblocked and blocked again, Tencent Cloud's basic network will be exposed to the attack traffic, which may affect other Tencent Cloud users. In addition, IP blocking is a service purchased from ISPs with restrictions on the total number of times and the frequency of unblocking.

### How can I unblock my IP earlier in case of emergency?
- You can upgrade the base protection capacity, so that the blocked IP can be unblocked automatically.
- You have three chances each day to [unblock the IP by yourself](https://intl.cloud.tencent.com/document/product/297/34090) in case of emergency.

### Why is there a limit on the number of chances for self-service unblocking? What are the restrictions?
Tencent Cloud pays ISPs for blocking attacked IPs, and ISPs impose limits on the number of times and frequency of unblocking.
Only **three** chances of self-service unblocking are provided for Anti-DDoS Advanced every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.


### How can I prevent my IP from being blocked?
When [purchasing an Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/15483), select an appropriate protection bandwidth based on the historical attack traffic data to ensure that the protection bandwidth is higher than the peak attack traffic.

### How can I prevent my IP from being blocked again?
You are recommended to increase the base protection bandwidth or elastic protection bandwidth to improve the protection capability. Enabling elastic protection can help you defend against high-traffic attacks. In addition, elastic protection is pay-as-you-go, which can reduce your security costs.
