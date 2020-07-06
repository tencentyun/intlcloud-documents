### Is Anti-DDoS Advanced available for non-Tencent Cloud users?
Yes. Anti-DDoS Advanced can protect all types of servers on the internet, including but not limited to those in Tencent Cloud, other clouds, and customer IDCs.
>ICP filing issued by MIIT is required for all domain names connected to Anti-DDoS Advanced in Mainland China.
### Does Anti-DDoS Advanced support wildcard domain names?
Yes. You can protect wildcard domain names by configuring website traffic forwarding rules.
Wildcard domain name resolution involves using wildcards (\*) as secondary domain names to allow all secondary domain names to point to the same IP. For example, you can configure \*.tencent.com.
### Does Anti-DDoS Advanced automatically add intermediate IPs to the security group?
No. You need to manually add the intermediate IP range to the CVM security group. If you have deployed firewall or other server security protection software on the real server, you also need to add the intermediate IP range to the whitelist to prevent business traffic from being affected due to blocking or speed limiting.
### Can I set a private IP as the real server IP in Anti-DDoS Advanced?
No. Anti-DDoS Advanced forwards traffic over the public network. Therefore, you cannot use a private IP.
### How long does it take for a real server IP update to take effect?
Changes to the real server IP protected by Anti-DDoS Advanced take effect in seconds.
### How long does it take for configuration modifications in the Anti-DDoS Advanced Console to take effect?
Changes to the Anti-DDoS Advanced service configuration take effect in seconds.
### Does Anti-DDoS Advanced support IPv6 protocol for traffic forwarding?
Currently, the IPv6 protocol is not supported.
### Does Anti-DDoS Advanced support HTTPS mutual authentication?
- For website applications, HTTPS mutual authentication is not supported.
- For non-website applications over TCP, HTTPS mutual authentication is supported.

### Does Anti-DDoS Advanced have packet capture files?
Anti-DDoS Advanced supports downloading packet capture files. For detailed directions, please see [Viewing Statistics Report
](https://intl.cloud.tencent.com/document/product/297/34099).
### How does Anti-DDoS Advanced deal with load balancing if multiple real server IPs are configured?
- Load balancing based on source IP hash is used for website applications.
- For non-website applications, load balancing based on weighted round robin is used to forward traffic to real server IPs in turn.

### How many forwarding ports and domain names are supported by one Anti-DDoS Advanced instance?
- Forwarding ports: 60 forwarding rules for TCP/UDP protocol are provided free of charge by default. The quantity can be increased.
- Domain names: 60 forwarding rules for HTTP/HTTPS protocol are provided free of charge by default. The quantity can be increased.

### What is business bandwidth? What will happen if this value is exceeded?
The business bandwidth purchased is for the entire Anti-DDoS Advanced instance. It refers to the inbound and outbound traffic of all normal businesses in the instance.
If your business traffic exceeds the free tier, it will trigger traffic speed limit, which may result in random packet loss. If this problem persists, please upgrade the business bandwidth in time.
>100 Mbps forwarding bandwidth is available free of charge for each Anti-DDoS Advanced instance.
### Does Anti-DDoS Advanced support session persistence?
Anti-DDoS Advanced support session persistence, which is not enabled by default. For non-website businesses, you can configure this feature in the consoles as instructed in [Configuring Session Persistence](https://intl.cloud.tencent.com/document/product/297/34097).
### Does Anti-DDoS Advanced support health check?
Health check is enabled for non-website businesses, which is recommended. You can modify this feature as instructed in [Configuring Health Check](https://intl.cloud.tencent.com/document/product/297/34096).

### WS is not enabled on my real server. After I bind my business to Anti-DDoS Advanced, why is the access to the real server slow?
Anti-DDoS servers have Window Scaling (WS) enabled by default. If this is not enabled on the real server, a delay will occur when the sliding window is filled up while receiving slightly larger files. You are recommended to enable WS for your real server.
