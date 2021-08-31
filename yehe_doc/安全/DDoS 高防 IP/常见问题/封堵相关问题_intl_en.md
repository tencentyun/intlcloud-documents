### Why is my IP blocked?
Tencent Cloud reduces costs of cloud services by sharing the infrastructure, with one public IP shared by many users. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, the target server IP needs to be blocked.

### Why can't my IP be unblocked immediately?
A DDoS attack usually does not stop immediately after the target IP is blocked, and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis.
Since IP blocking takes effect in ISP network, Tencent Cloud cannot monitor whether the attack traffic has stopped after the attacked public IP is blocked. If the IP is unblocked but the attack is still going on, the IP will be blocked again. During the gap between the IP being unblocked and blocked again, Tencent Cloud's classic network will be exposed to the attack traffic, which may affect other Tencent Cloud users. In addition, IP blocking is a service purchased from ISPs with restrictions on the total number of times and the frequency of unblocking.

### How can I unblock my IP earlier in case of emergency?
You have three chances each day to unblock the IP by yourself on the protection overview page in the console if you need to resume your business urgently.

### Why is there a limit on the number of chances for self-service unblocking? What are the restrictions?
Tencent Cloud pays ISPs for blocking attacked IPs, and ISPs impose limits on the number of times and frequency of unblocking.
Only **three** chances of self-service unblocking are provided for Anti-DDoS Advanced every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day.


### How can I prevent my IP from being blocked?
When purchasing an Anti-DDoS Advanced instance, you can select the appropriate protection bandwidth based on the historical attack traffic data to ensure that the maximum protection bandwidth is higher than the peak historical attack traffic bandwidth.

### How can I prevent my IP from being blocked again?
You are recommended to enable elastic protection and set a high elastic protection bandwidth to defend against large-traffic attacks. In addition, elastic protection is pay-as-you-go on a daily basis, which can help reduce your security costs.
