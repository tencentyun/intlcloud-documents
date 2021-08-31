Tencent Cloud NAT Gateway maps EIPs and ports to private IPs and ports of CVM instances, allowing VPC CVM instances without any public IP to access and be accessed over the public network.
NAT Gateway features Source Network Address Translation (SNAT), Destination Network Address Translation (DNAT), gateway traffic control, traffic alarm, bandwidth packages, Anti-DDoS, automatic disaster recovery, and a lot more.

### SNAT
SNAT makes it possible for multiple CVMs in the VPC to actively access the public network through the same public IP address. A single NAT Gateway instance supports a maximum forwarding capability of 5 Gbps.
You can bind multiple EIPs to NAT Gateway and allow CVM instances to access the public network through a random EIP. If you want to specify an EIP for the public network access, add it to the SANT address pool, so that CVMs can only access the public network through the EIP in the address pool.

### DNAT
DNAT is used to map the public IP addresses, protocols, and ports to private IP addresses, protocols, and ports of the CVM in the VPC, so that services on the CVM can be accessed from the internet.

### Bandwidth Packages
NAT Gateway can be used with [IP bandwidth packages](https://intl.cloud.tencent.com/document/product/684/15245) to share the public network bandwidth among multiple IP addresses after you binding EIPs to NAT Gateway and adding them to IP bandwidth packages. This is suitable for applications where traffic can be staggered, effectively reducing bandwidth costs.

### Gateway Traffic Control
You can enable the traffic control feature for NAT Gateway to control the bandwidth from a private IP address to the NAT Gateway. This feature provides **monitoring** and **control** capabilities at **IP-gateway** granularity. The visualization helps network OPS personnel get a clear picture of the gateway traffic. The speed limiting capability at IP-gateway granularity helps block unhealthy traffic and protect key businesses.

### Traffic Alarm
You can customize traffic alarms for NAT Gateway. When a metric value exceeds its threshold, alarm notifications are sent to you automatically via emails and SMS message. Monitoring and alarm services are free of charge, helping you quickly locate problems.

### Anti-DDoS
Anti-DDoS Pro defends against DDoS and CC attacks with a protection bandwidth capability of up to 310 Gbps. You can bind an Anti-DDoS Pro instance to the NAT Gateway to enhance security.

### Automatic Disaster Recovery
NAT Gateway features dual-server hot backup and automatic disaster recovery. Services on the failed server will be imperceptibly switched to the other server to maintain availability up to 99.99% and ensure your service stability.
