

### Can the real server IP added to WAF be the private IP of a Tencent Cloud CVM instance?
When adding a domain name to WAF, the real server address must be a domain name or a public IP, such as CVM public IP, CLB public IP, or Egress IP of other local IDCs, while a CVM private IP is not supported.


### What is a forwarding IP used for?
A forwarding IP is automatically assigned after the protected domain name is configured in SaaS WAF. When forwarding traffic to the client’s real server, WAF will use the forwarding IP as source address. To achieve better protection, you need to add the forwarding IP to a trusted list on the server. It is recommended allowing only access traffic from the WAF forwarding IP to the real server.


### How many real server IPs can be set for one protected domain name in WAF?
Up to 20 real server IPs can be set for one protected domain name in WAF.

### How does the traffic balancing work when multiple real servers are configured in WAF?
If multiple forwarding IPs are configured, WAF achieves load balancing for access requests by polling.


### Does WAF automatically add a forwarding IP range to a security group?
WAF does not automatically add a forwarding IP range to a security group. To do so, please see [Getting Started](https://intl.cloud.tencent.com/document/product/627/18635).
