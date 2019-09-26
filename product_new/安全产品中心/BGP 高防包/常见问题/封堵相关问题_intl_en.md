## What do I do if the IP protected by Anti-DDoS Pro is blocked? 
If the elastic protection bandwidth of the Anti-DDoS Pro instance in use is not adjusted to the highest, you can change the bandwidth in **Anti-DDoS Console** to improve the elastic protection capability against larger attack traffic. 
In addition, you have three times each day to unblock the IP by yourself. In emergencies, you can perform [self-recovery](https://intl.cloud.tencent.com/document/product/1029/31758). 

## Why is my IP blocked when under attack? 
Tencent Cloud reduces the cost by sharing the infrastructure, with one public IP being shared among all users. When a large traffic attack occurs, the entire Tencent Cloud network may be affected, in addition to the attacked servers. To protect other servers and to ensure the network stability, we need to block the attacked server IP. 

## Why do you charge for Anti-DDoS Advanced traffic? 
DDoS attacks have negative effects on not only the targets but also the entire cloud network, affecting other non-attacked users in the cloud as well. Moreover, building the anti-DDoS system costs high, including the cleansing cost and the bandwidth cost. Specifically, the largest expense is bandwidth and it is calculated based on the total traffic. No difference exists between normal traffic and attack traffic in terms of the bandwidth cost.  
Therefore, although Tencent Cloud can afford limited free DDoS Basic service for all users, we have to block inbound public network traffic of the attacked servers when the attack traffic exceeds the free quota. 

## Why can't my IP be unblocked immediately after the attack ends? 
A DDoS attack usually does not stop immediately after the IP blocking and the attack duration is uncertain. Tencent Cloud security team sets the default blocking period based on big data analysis. 
Because the IP blocking takes effect in the carrier's network, Tencent Cloud is unable to monitor whether the attack traffic flow has been stopped. If the IP is recovered but the attack is still going on, the IP will be blocked again. A gap exists between the recovery and the re-blocking that the attack traffic can take the advantage of directly entering the Tencent Cloud's basic network, resulting in negative effects on other cloud users. In addition, the IP blocking is a service Tencent Cloud purchases from carriers with limited numbers of the unblocking and blocking frequency.  

## How can I unblock the IP earlier in case of an emergency? 
1. Starting or upgrading the elastic protection capability and adjusting the elastic protection to the maximum value will allow for earlier automatic unblocking. 
2. Three chances of self-unblocking are provided for users with Anti-DDoS Pro every day. In case of emergencies, you can [self-unblocking](https://intl.cloud.tencent.com/document/product/1029/31758). 

## Why is there a limit on the number of self-unblocking? What are the limitations? 
Tencent Cloud pays carriers for blocking attacked IPs, and carriers impose limits on the time and frequency of unblocking. 
Only **three** chances of self-unblocking are provided for users with Anti-DDoS Pro every day. The system resets the self-unblocking chances daily at midnight. Unused chances cannot be accumulated to the following day. 

## How do I connect to a blocked server? 
If data migration or other operations are required, you may use either of the following methods to connect to the blocked server: 
- Connect to the blocked server using the private IP through another CVM in the same region. 
- In [CVM Console](https://console.cloud.tencent.com/cvm), click **Login** in the line of the blocked server to connect through browser VNC. 

## How can I prevent the IP from being blocked? 
When you [purchase Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/31748), you can choose an appropriate base protection bandwidth or enable elastic protection at the same time based on the historical attack traffic data to ensure that the maximum protection bandwidth exceeds the attack bandwidth. 

## How can I prevent my anti-DDoS IP from being blocked again? 
You are advised to upgrade the elastic protection bandwidth to improve the defense capability. Enabling the elastic protection can protect you from large traffic attacks. In addition, the elastic protection is charged flexibly by day on demand, reducing your security cost effectively. 

