Tencent Cloud provides you with various methods to access the Internet, such as through a common public IP address, EIP, NAT gateway, and Cloud Load Balancer (CLB). 

## Common Public IP Addresses
When creating a CVM instance, you can assign a common public IP address to the instance. The system will assign an IP address to your CVM to enable it to access the Internet and also be accessible through the Internet. 
Common public IP addresses cannot be dynamically bound or unbound with resources such as CVMs, but you can convert them to EIPs. For details, see [Converting Public IP Addresses into EIPs](https://intl.cloud.tencent.com/document/product/213/16586).

## Elastic IP Addresses
Unlike public IP addresses that need to be applied for and released with CVMs, elastic IP addresses (EIPs) are independent cloud resources that are decoupled from the CVM lifecycle and can be operated separately. 
For information on how to apply for, bind, and release EIPs, see [EIPs - Steps](https://intl.cloud.tencent.com/document/product/213/16586). 
EIPs offer the following advantages: 
- Independent cloud resources 
You can operate EIPs independently, without needing to purchase them with CVMs. 
- Elastic binding and unbinding with resources 
EIPs can be bound and unbound with CVMs and other resources at any time. 

## NAT Gateways
A NAT gateway provides the SNAT and DNAT features, which enables you to easily establish an Internet egress and provide services for CVMs in a VPC to access the Internet with the same public IP address. 
For information on how to configure the NAT gateway, see [NAT Gateways - Operation Overview](https://intl.cloud.tencent.com/document/product/1015/30235).
NAT gateways offer the following advantages: 
- Secure Internet access 
NAT gateways provide the SNAT and DNAT features to hide the IP addresses of CVMs in a VPC during Internet communication, ensuring security. 
- High availability 
NAT gateways feature master/slave hot backup, automatic hot switching, and quick forwarding with a rate up to 5 Gbps. In addition, they support large-scale Internet applications. 
- Flexible configuration 
You can modify NAT gateway specifications as required at any time. 

## Cloud Load Balancers
A Cloud Load Balancer (CLB) distributes traffic to multiple CVMs to enhance the external service capabilities of application systems. It eliminates single points of failure to ensure highly available application systems.
For information on how to purchase and configure a CLB, see [CLBs - Getting Started](https://intl.cloud.tencent.com/document/product/214/8975).
CLBs offer the following advantages: 
- High-performance single cluster 
A CLB cluster consists of multiple physical servers, with an availability of up to 99.95%. The cluster system can remove faulty instances and select healthy instances to ensure the proper running of services on the real server.
- High security and stability
With the BGP anti-DDoS system, the CLB can defend against most network attacks (such as DDoS attacks) and cleanse traffic attacks in seconds, preventing blocked IP addresses or full bandwidth consumption.

## Public Gateways
A public gateway is a CVM with the forwarding feature enabled. In a VPC, CVMs without a public IP address can access the Internet through public gateways on different subnets. Public gateways can covert the source addresses of Internet traffic from other CVMs to their own IP addresses.
For information on how to configure a public gateway, see [Configuring Public Gateways](https://intl.cloud.tencent.com/document/product/215/33404).
