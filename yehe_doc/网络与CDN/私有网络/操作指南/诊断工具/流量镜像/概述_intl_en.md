Traffic mirror provides a traffic collection service that filters and copies desired traffic from the specified network interface to CVM instances in the same VPC. This feature is applicable to use cases including security audit, risk monitoring, troubleshooting and business analysis.
> ?However, traffic mirror consumes CVM resources such as CPU, memory and bandwidth pro rata. For example, if you mirror a network interface that has 1 Gbps of inbound traffic and 1 Gbps of outbound traffic. In this case, the instance needs to handle 1 Gbps of inbound traffic and 3 Gbps of outbound traffic (1 Gbps for the outbound traffic, 1 Gbps for the mirrored inbound traffic and 1 Gbps for the mirrored outbound traffic).

## Procedure
The following are key components of a traffic mirror, together with its workflow.
- Source: the specified ENI in the VPC that applies the filter rules such as network, collection range, collection type and traffic filtering.
- Target: the receiving IPs that get the collected traffic.
![](https://main.qcloudimg.com/raw/37ff00d3d5021bb7340d2b233a3182dc.png)

## Use Cases
### Security auditing
A running system may occur unhealthy network traffic or generate an error message due to software exception, hardware fault, computer virus or improper use. To locate causes of these issues, you can use traffic mirror to analyze the network messages.

### Intrusion checking
To ensure the confidentiality, integrity and availability of network system resources, you can use traffic mirror to copy traffic to CVM clusters for real-time analysis.

### Business analysis
Use traffic mirror to clearly and visually present the business traffic mode.
