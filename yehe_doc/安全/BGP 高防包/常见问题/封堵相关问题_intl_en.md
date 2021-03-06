### What should I do if the IP protected by Anti-DDoS Pro is blocked? 
You have three chances each day to unblock the IP by yourself on the protection overview page in the console if you need to resume your business urgently. 

### Why is my IP blocked? 
Tencent Cloud reduces costs of cloud services by sharing the infrastructure. All users share a single internet exit point. When a high-traffic attack occurs, the entire Tencent Cloud network may be affected, not only the attacked servers. To protect other users and ensure the network stability, the attacked server IP needs to be blocked. 

### Why can't my IP be unblocked immediately? 
A DDoS attack usually does not stop immediately after the target IP is blocked and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis. 
Since IP blocking takes effect in ISP network, Tencent Cloud cannot monitor whether the attack traffic has stopped after the attacked public IP is blocked. If the IP is unblocked but the attack is still going on, the IP will be blocked again. During the gap between the IP being unblocked and blocked again, Tencent Cloud's classic network will be exposed to the attack traffic, which may affect other Tencent Cloud users. In addition, IP blocking is a service purchased from ISPs with restrictions on the total number of times and the frequency of unblocking. 

### Why is there a limit on the number of chances for self-service unblocking? What are the restrictions? 
Tencent Cloud pays ISPs for blocking attacked IPs, and ISPs impose limits on the number of times and frequency of unblocking. 
Only **three** chances of self-service unblocking are provided for Anti-DDoS Pro every day. The system resets the chance counter daily at midnight. Unused chances cannot be accumulated for the next day. 

### How do I connect to a blocked server? 
If you need to perform operations such as data migration, you may use either of the following methods to connect to the blocked server: 
- Connect to the blocked server by using the private IP through another CVM instance in the same region. 
- In the [CVM Console](https://console.cloud.tencent.com/cvm), click **Log In** in the row of the blocked server and connect by using the VNC method.   
