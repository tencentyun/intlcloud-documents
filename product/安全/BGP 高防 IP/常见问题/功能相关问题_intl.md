[//]: # (chinagitpath:XXXXX)

## Is Anti-DDoS Advanced available to non-Tencent Cloud users?
Yes. Anti-DDoS Advanced is available to any servers with access to internet, including but not limited to customer IDCs, servers deployed on Tencent Cloud and other cloud providers.
>! As required by MIIT, ICP filing is a must for all domain names in Mainland China.

## Does Anti-DDoS Advanced support wildcard domain names?
Yes. You can enabling it by configuring website traffic forwarding rules.
Wildcard domain name resolution involves using wildcards (\*) as secondary domain names to allow all secondary domain names to point to the same IP. For example, you can configure \*.tencent.com.

## Does Anti-DDoS Advanced automatically add intermediate IPs to the security group?
No. You need to manually add the intermediate IP range to the CVM security group. If you have deployed firewall or other host security protection software on the real server, you also need to add the intermediate IP range to the whitelist to prevent the traffic from being affected due to the blocking of these IPs or speed restriction.

## Can I set a private IP as the real server IP?
No. Anti-DDoS Advanced forwards traffic via public network. Therefore, you can't enter a private IP.

## How long does the modification of real server IP take to work?
It takes effect within seconds.

## How long does the configuration change on console take to work?
It takes effect within seconds.

## Does Anti-DDoS Advanced support IPv6 protocol for traffic forwarding?
No.

## Does Anti-DDoS Advanced support HTTPS bidirectional authentication?
- For website applications, HTTPS bidirectional authentication is not supported.
- For non-website applications using TCP, HTTPS bidirectional authentication is supported

## Can I download dump files?
Yes. [Click here
](Https://cloud.tencent.com/document/product/1014/31112) for details.

## How does Anti-DDoS Advanced deal with load balancing if multiple real server IPs are configured?
- For website applications, source IP hash algorithm is used for load balancing.
- For non-website applications, weighed polling is used to forward traffic to the real server IPs in turn.

## How many forwarding ports and domain names are supported by each Anti-DDoS Advance service pack?
- Forwarding ports: Up to 60 rules for TCP/UDP protocol.
- Domain names: Up to 60 rules for HTTP/HTTPS protocol.

## What is service bandwidth？ What will happen if this value is exceeded?
The service bandwidth purchased is for the entire Anti-DDoS Advanced instance. It refers to the inbound and outbound traffic of all normal services of this IP.
In case the forwarding bandwidth is exceeded, traffic speed will be limited and packet loss can occur
>? 100M of free forwarding traffic is available for each Anti-DDoS Advanced service pack.

## Does Anti-DDoS Advanced support session persistence?
Yes. It allows a session to persist for 600 seconds.

## Why is my protective IP blocked when it’s being attacked?
Tencent Cloud reduces the cost of using cloud by sharing infrastructure, with its public network egress shared among all users. When a high-traffic attack occurs, in addition to the target of attack, the entire Tencent Cloud network may be affected. In order to prevent the attack from affecting other users who are not attacked and to ensure the stability of the entire cloud network, blocking is needed.

## Why doesn’t Anti-DDoS Advance provide unlimited and free traffic?
DDoS attacks affect not only the attacked customer, but also the entire cloud network, and other customers on Tencent Cloud. Anti-DDoS protection involves high bandwidth cost and cleansing cost. Bandwidth cost, which counts a larger part of the total cost, includes the normal traffic and attack traffic.
Therefore, Tencent Cloud can afford to provide cloud service users with free anti-DDoS base protection service. When the attack traffic exceeds the free quota, Tencent Cloud will block the public network traffic flowing to the attacked IP.

## Why can't my IP be recovered immediately after the attack ends?
Usually a DDoS attack continues for a period of time and will not stop immediately after blocking. This means that its duration is uncertain. Tencent Cloud security team will set the default blocking duration based on big data analysis results.
As the blocking takes effect within the ISP's network, when the attacked IP is blocked, Tencent Cloud is unable to monitor whether the attack traffic has stopped. If the IP is recovered when the attack still persists, the IP will be blocked again. However there’s a gap between the attack traffic will flow into Tencent Cloud's basic network directly during the period between the removal of blocking and the re-blocking, affecting other users in the cloud.

## How can I restore the business without removing blocking in an emergency?
It’s recommended to purchase a service pack with higher capacity and configure the original forwarding rules.
If your server is not deployed on Tencent Cloud, it’s recommended to change the real server IP, [purchase](https://cloud.tencent.com/document/product/1014/31101) and use [Anti-DDoS Advanced](https://cloud.tencent.com/document/product/1014/31091) to ensure the normal operation of your business.

## How can I recover the blocked IP earlier in case of an emergency?
You can upgrade the base protection capacity, in this case, the blocked IP is recovered automatically.

## Why are there limits on the count and frequency of manual recovering of blocked IP?
Tencent Cloud is charged by ISPs for blocking attacked IPs. And ISPs impose limits on the time and frequency of canceling unblocking.
Each user has **three** chances to recover their anti-DDoS IP manually a day. The quota is reset at 00:00 every day, and unused quota is not accumulated.

## How do I connect to a blocked server?
There are three ways to connect to a blocked server:
- Connect to the blocked server from another CVM in the same region via the private IP;
- Log in to [CVM console](https://console.cloud.tencent.com/cvm), select the blocked CVM and click **Log In** to connect to it via VNC from browser.
- Log in to the [CVM console](https://console.cloud.tencent.com/cvm), bind the blocked server with a new EIP, through which you can connect to the server.

## How can I prevent the IP from being blocked?
Set a proper protection bandwidth while [purchasing Anti-DDoS Advanced](https://cloud.tencent.com/document/product/1014/31101), ensuring that the maximum protection bandwidth is greater than the attack traffic peak as can as possible.

## How can I prevent my anti-DDoS IP from being blocked again?
It is recommended to upgrade the base protection bandwidth or elastic protection bandwidth. Elastic protection can help you withstand high-traffic attacks, and is billed by traffic on a daily basis, so as to save your cost.

