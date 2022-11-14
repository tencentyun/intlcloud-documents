
### What is Cloud Firewall? [](id:question1)
Tencent Cloud Firewall (CFW) is a SaaS firewall based on the public cloud environment that provides network perimeter protection and addresses security and management needs for unified access control and log audit. In addition to the features of traditional firewalls, CFW supports multi-tenancy and elastic scaling and is an essential network security infrastructure for cloud migration.

### Can CFW protect assets not running on Tencent Cloud?	 
No. CFW only protects IP assets under Tencent Cloud accounts.

### What's the difference between CFW and security group?	[](id:question2)
Cloud Firewall and Security Group are standalone systems. When the Internet service is enabled for a public EIP, traffic is allowed only when it is allowed by the policies of both systems.
- Control scope of the two systems is different. Edge firewall controls the access traffic of public IP addresses, while security group controls all traffic of CVM NIC.
- Application scope of the two systems is different. Security group is applied to instances, while CFW is applied to public IPS, NAT edge protection, and peer connections or CCN between VPCs.
- Security group ACL is the most fundamental feature of CFW, and its more important capabilities are log audit of full traffic and real-time interception of Intrusion Protection System (IPS).

### What's the difference between CFW and WAF?	
- Web Application Firewall (WAF) only protects web services and prevents attacks from outside to inside. It does not monitor or prevent malicious outgoing access of services.
- CFW protects all services. It not only provides basic prevention from web vulnerabilities, but also supports detection of outgoing access from inside to outside. In addition, CFW will automatically intercept compromised servers and malicious outgoing access.

### What's the difference between CFW and Security Ops center in terms of traffic threat awareness?
CFW is integrated with enterprise-level IPS and IDS features, and delivers virtual patching on zero-day vulnerabilities within hours without the need to upgrade or restart services. These capabilities are not supported by Security Ops center.

### Can CFW protect CDN or COS?	
No. CFW does not protect SaaS services such as CDN, COS, high defense IP, SaaS-WAF, and CDB, except for database services.

### Does traffic go through CFW before other products? Does CFW protect CDN traffic?
- IP addresses of CDN nodes belong to corresponding CDN carriers, which are beyond the protection scope of CFW. Only CDN traffic that goes back to CLB or CVM will be detected by CFW. High defense IP that goes back to CLB will also go through CFW, with back-to-source addresses of these IP nodes displayed.
- For the current version, only the BGP IP address type is supported. The IP addresses of China Mobile, China Unicom, and China Telecom are not supported currently. CFW will automatically ignore the IP addresses of China Mobile, China Unicom, and China Telecom during identification of user assets.

### Does CFW have QPS limitations?
CFW is a SaaS service without limitations on concurrency, creation, and QPS of traditional firewalls. Actual throughput is the only one performance indication of CFW.

### Does external inbound traffic go through CFW or WAF first? [](id:question3)
#### For inbound traffic
- SaaS-WAF and CFW work together as the overall perimeter protection layer for cloud security. WAF offers protection for encrypted HTTPS traffic, while Cloud Firewall integrates Intrusion Prevention System (IPS), and virtual patching to protect unencrypted traffic.
- SaaS-WAF and CFW work in parallel. After the traffic passes through the SaaS WAF, it does not go through CFW. For serial deployment, CLB-WAF is required. In this case, traffic goes through CFW and then CLB-WAF.
>? Traffic that goes back to CLB or CVM will not go through CFW as well. Outgoing access of source CVM nodes can be identified and detected by using the NAT firewall.

#### For outbound traffic
- The NAT firewall can help control outgoing requests based on CVM and control access based on domain name. With Tencent Threat Intelligence, it can automatically block any malicious IP addresses or domain names for outgoing requests.
- If the NAT firewall is not enabled, access control for outbound traffic is only available with the edge firewall after the traffic goes through the NAT gateway. From the perspective of Cloud Firewall, the traffic comes from a public IP address.
