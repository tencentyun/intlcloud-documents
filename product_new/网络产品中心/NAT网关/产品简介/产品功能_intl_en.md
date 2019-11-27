Tencent Cloud NAT Gateway features Source Network Address Translation (SNAT), Destination Network Address Translation (DNAT), gateway traffic control, traffic alarm, shared bandwidth packages, Anti-DDoS, automatic disaster recovery, and a lot more.
### SNAT
SNAT makes it possible for multiple CVMs on the VPC to actively access the Internet through the same public IP address. A single NAT Gateway instance supports a maximum forwarding capability of 5 Gbps.
### DNAT
DNAT is used to map the private IP addresses, protocols, and ports of the CVM in the VPC to public IP addresses, protocols, and ports, so that services on the CVM can be accessed from the internet.
## Gateway Traffic Control
You can enable the gateway traffic control feature for NAT gateways. Gateway traffic control restricts the bandwidth between a private IP address and a NAT gateway. Gateway traffic control provides the "monitoring" and "control" capabilities at the IP-gateway granularity, enabling refined gateway traffic visualization that helps OPS personnel get insight into traffic. In addition, the speed limiting capability at the IP granularity helps make troubleshooting faster, enables the blocking of abnormal traffic, and protects key businesses.
### Traffic Alarm
Custom traffic alarms can be set up to enable advance alerting for risks, with alarm messages automatically sent via emails and SMS messages when a metric exceeds its threshold. Both the monitoring and alarm functions are free of charge, enabling you to quickly locate problems once they occur.
### Shared Bandwidth Packages
NAT gateways can be used with shared bandwidth packages to share the public network bandwidth among multiple IP addresses, which can be used for staggering the traffic among different applications, effectively reducing bandwidth costs.
### Anti-DDoS
Anti-DDoS provides DDoS and CC protection with an extremely high bandwidth, offering a BGP protection bandwidth up to 310 Gbps. Anti-DDoS instance can be bound to the NAT gateway requiring protection to achieve security enhancement.
### Automatic Disaster Recovery
NAT Gateway provides master/slave hot backup and automatic disaster recovery, enabling automatic switching in case of a single point of failure with imperceptible impact on the service. Service availability of up to 99.99% keeps your business running smoothly.
	







