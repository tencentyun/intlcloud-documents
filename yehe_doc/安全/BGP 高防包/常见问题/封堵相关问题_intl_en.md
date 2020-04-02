### What should I do if the IP protected by Anti-DDoS Pro is blocked? 
If the elastic protection bandwidth of the Anti-DDoS Pro instance in use is not adjusted to the highest, you can increase the bandwidth in Anti-DDoS Pro Console to improve the elastic protection capability against attacks of larger traffic. 
In addition, you have three times each day to [unblock the IP by yourself](https://intl.cloud.tencent.com/document/product/1029/31758). 

### Why is my IP blocked? 
Tencent Cloud reduces costs of using clouds by sharing the infrastructure, with one public IP shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, not only the target servers. To protect other users and ensure network stability, we have to block the target server IP. 

### Why isn’t anti-DDoS service always free? 
DDoS attacks not only threaten the targets but also the entire cloud network, affecting non-attacked Tencent Cloud users as well. Also, DDoS protection incurs high costs, including cleansing costs and bandwidth costs, in which bandwidth costs the most. Bandwidth costs are calculated based on the total amount of traffic; there is no difference between costs incurred by normal traffic and attack traffic. 
Therefore, Tencent Cloud provides Anti-DDoS Basic service free of charge for all users. But once the attack traffic exceeds the free quota, we will have to block the attacked IP from all public network access. 

### Why can't I unblock my IP immediately? 
A DDoS attack usually does not stop immediately after the target IP is blocked and the attack duration varies. Tencent Cloud security team sets the default blocking duration based on big data analysis. 
Since IP blocking takes effect in ISPs’ network, Tencent Cloud will be unable to monitor whether the attack traffic has stopped after the attacked public IP is blocked. If the IP is recovered but the attack is still going on, the IP will be blocked again. During the gap between the IP being recovered and blocked again, Tencent Cloud's basic network will be exposed to the attack traffic, which may affect other users in Tencent Cloud. In addition, IP blocking is a service offered by ISPs with limitations on the total number of times and the frequency of unblocking.  

### How can I unblock the IP earlier in case of an emergency? 
1. You can upgrade the base protection bandwidth, in this case, the blocked IP is recovered automatically. 
2. You have three times each day to [unblock the IP by yourself](https://intl.cloud.tencent.com/document/product/1029/31758). 

### Why is there a limit on the number of self-unblocking? What are the limitations? 
Tencent Cloud pays carriers for blocking attacked IPs, and carriers impose limits on the time and frequency of unblocking. 
Only **three** chances of self-unblocking are provided for users with Anti-DDoS Pro every day. The system resets the self-unblocking chances daily at midnight. Unused chances cannot be accumulated to the following day. 

### How do I connect to a blocked server? 
If you need to perform operations such as data migration, you may use either of the following methods to connect to the blocked server: 
- Connect to the blocked server using the private IP through another CVM in the same region. 
- In [CVM Console](https://console.cloud.tencent.com/cvm), click **Log In** in the row of the blocked server, and connect using the VNC method. 

### How can I prevent my IP from being blocked? 
When you [purchase Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/31748), you can set an appropriate protection bandwidth based on the historical attack traffic data to ensure that the bandwidth of most attacks is lower than the maximum protection bandwidth. 

### How can I prevent my IP from being blocked again? 
We recommend you upgrade the base protection bandwidth or elastic protection bandwidth. Elastic protection can help defense against high-traffic attacks, and you only pay for what you use per day, which reduces your cost. 
