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


