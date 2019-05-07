## Is Anti-DDoS Advanced available for non-Tencent Cloud users?
Yes. Anti-DDoS Advanced is available for any servers with access to the internet, including, but not limited to customer IDC, servers deployed inside or outside the Tencent Cloud.
>  ICP  license issued by MIIT  is required for all domain names hosted in Mainland China.

## Does Anti-DDoS Advanced support wildcard domain names?
Yes. You can enable it by configuring website traffic forwarding rules.
Wildcard domain name resolution involves using wildcards \\* as secondary domain names that allow all secondary domain names to point to the same IP. For example, you can configure \\*.tencent.com.

## Does Anti-DDoS Advanced automatically add intermediate IPs to the security group?
No. You need to manually add the intermediate IP range to the CVM security group. If you have deployed firewall or other host security protection software on the real server, you also need to add a range for the intermediate IP to the whitelist to prevent the traffic from being affected due to the blocking or speed restriction.

## Can I set a private IP as the real server IP?
No. Anti-DDoS Advanced forwards traffic via public network. Therefore, you cannot use a private IP.

## How long does it take for the real server IP update to take effect?
It takes effect in seconds.

## How long does it take for the change of configuration in the console to take effect?
It takes effect in seconds.

## Does Anti-DDoS Advanced support IPv6 protocol for traffic forwarding?
No.

## Does Anti-DDoS Advanced support HTTPS bidirectional authentication?
- For website applications, HTTPS bidirectional authentication is not supported.
- For non-website applications using TCP, HTTPS bidirectional authentication is supported

## How does Anti-DDoS Advanced IP perform load balancing if multiple real server IPs are configured?
- Source IP hashing load balancing is used for website applications.
- For non-website applications, weighted round robin load balancing is used to forward traffic to real server IPs.

## How many forwarding ports and domain names are supported by each Anti-DDoS Advanced instance?
- Forwarding ports: Up to 60 rules for TCP/UDP protocol by default.
- Domain names: Up to 60 rules for HTTP/HTTPS protocol by default.

## What is service bandwidth?  What will happen if this value is exceeded?
The service bandwidth purchased is for the entire Anti-DDoS Advanced instance. It refers to the and outbound traffic of all normal services of this IP.
If the forwarding bandwidth exceeds the service bandwidth, the traffic will slow down and packet loss may occur.
> 100M free forwarding traffic is available for each Anti-DDoS Advanced instance.

## Does Anti-DDoS Advanced support conversation persistence?
Yes. It keeps a conversation available for 600 seconds.
## Why is my Anti-DDoS Advanced IP blocked when it’s being attacked?
Tencent Cloud reduces the cost by sharing infrastructure, with a public IP shared among all users. 
When a massive traffic attack occurs, the entire Tencent cloud network may be affected, in addition to the target servers.  In order to prevent non-targeted servers from being affected and ensure network stability, we need to block the targeted server IP.

## Why isn’t unlimited Anti-DDoS Advanced traffic free?
DDoS attacks have negative effects on not only the targets but also the entire cloud network, affecting other non-targeted users in the cloud as well. Moreover, the cost of building the anti-DDoS system is very high, including the cleaning cost and the bandwidth cost. Specifically, the largest expense is bandwidth and it is calculated based on total traffic - there is no difference between normal traffic and attack traffic in terms of the bandwidth cost. Therefore, although Tencent Cloud can afford limited free DDoS Basic service for all users,  we have to block inbound public network traffic of the targeted servers when attack traffic exceeds the free quota.

## Why can't my IP be recovered immediately after the attack ends?
A DDoS attack usually does not stop immediately after the IP blocking and how long it lasts is uncertain. Tencent Cloud security team set the default blocking period based on big data analysis. Since the IP blocking takes effect in the ISP's network, Tencent Cloud is unable to monitor whether or not the attack traffic flow has been stopped. If the IP is recovered while the attack is still going on, the IP will be blocked again, where there’s a gap between the recovery and the re-blocking that the attack traffic can take advantage of to directly enter the Tencent Cloud's basic network, resulting in negative effects on other cloud users.  In addition, the IP blocking is a service Tencent cloud purchase from ISPs with limited numbers of blocking and blocking frequency. 

## How can I restore the business while my IP is being blocked?
We recommend that you upgrade your service pack to one has the higher defense capacity and configure the original forwarding rules.
If your server is not deployed on Tencent Cloud, we recommend you change the real server IP, [purchase](https://intl.cloud.tencent.com/document/product/297/15483) and use [Anti-DDoS Advanced](https://intl.cloud.tencent.com/document/product/297/16497) to ensure the normal operation of your business.

## How can I recover the blocked IP earlier in case of an emergency?
You can upgrade the base protection capacity so that the blocked IP can be recovered automatically.

## Why is there a limit on the number of self-unblock? What are the restrictions?
Tencent Cloud pays ISPs for blocking attacked IPs, and ISPs impose limits on the time and frequency of canceling unblocking.
Each user has **three** chances to recover their anti-DDoS IP manually per day. The quota is reset at 00:00 every day, and the unused quota is not accumulated.

## How do I connect to a blocked server?
There are three ways to connect to a blocked server:
- Connect the blocked server via the private IP through another CVM in the same region;
- Log in to [CVM console](https://console.cloud.tencent.com/cvm), select the blocked CVM and click **Log In**  and connect via browser VNC.
- Log in to the [CVM console](https://console.cloud.tencent.com/cvm), associate the blocked server with a new EIP.  Now you are able to connect to the blocked server.

## How can I prevent the IP from being blocked?
When you [purchasing Anti-DDoS Advanced (https://cloud.tencent.com/document/product/1014/31101)], select an appropriate protection bandwidth based on the historical attack traffic data to ensure that the protection bandwidth is higher than the attack traffic peak.

## How can I prevent my anti-DDoS IP from being blocked again?
We recommend you upgrade the base protection bandwidth or elastic protection bandwidth. Elastic protection can help defense against high-traffic attacks, and you only pay for what you use per day, which reduces your cost.
