On [CLB purchase page](https://buy.cloud.tencent.com/lb?rid=1&type=2&vpcId=vpc-5wru9vot), you can select CLB instances of different attributes. This document describes how to purchase instances based on business scenarios.
## Regions
- We recommend selecting the region closest to your client to reduce delay and accelerate the download speed.
- CLB can only forward traffic to CVM instances in the same region. Please select the region where your CVM instance is located before creating a CLB instance.
- CLB can forward traffic to CVM instances in multiple availability zones in the same region. For example, a CLB instance in Beijing can forward traffic to CVM instances in Beijing Zone 1, Beijing Zone 2, and Beijing Zone 3.
- A public network CLB (formerly "application CLB") instance supports cross-region binding of CVM. You can select the region of real servers and bind them across VPCs or regions. For example, you can bind a CLB instance in Beijing to a CVM instance in Shanghai to forward the client traffic to the latter. For more information, please see [CLB Instance Cross-Region Binding](https://cloud.tencent.com/document/product/214/12014).

## Instance Types
CLB instances can be classified into two types: CLB (formerly "application CLB") and classic CLB. CLB covers all features of classic CLB. Based on product features and performance, we recommend CLB. For a detailed comparison, please see [Instance Types](https://cloud.tencent.com/document/product/214/8847).

## Network Types
### Public network CLB
If you need to use CLB to distribute requests from the public network, please select "Public Network".
Public network CLB instances obtain requests from the client via the internet and distribute them to the bound real servers. After you create a public network CLB instance, Tencent Cloud will assign it a VIP address to be resolved by DNS server. Public network CLB allows users to add CNAME and A records, and map them to custom domain names. VIPs of public network CLB instances are fixed public IPs. They can receive HTTP, HTTPS, TCP, UDP, and other requests from the client.
- **Use Cases**
  - A server cluster is used to provide services to public networks. A unified entry is required, while requests from users of public networks should be assigned to server clusters.
  - Users of different ISPs are connected to networks closest to them to accelerate network access.
- **Public VIP types**  
  - Regular IP: Regular BGP IP, which is suitable for users want to balance the network quality and cost.
  - Single-line IP: Accessing the public network via a single ISP, which is low-cost and convenient for self-scheduling.
- **Billing**
  - For a bill-by-CVM account, only the instance fee is charged for purchasing a public network CLB instance. The service fees incurred by public network bandwidth and traffic are charged on its real server. For more information, please see [Bill-by-CVM Account Billing Description](https://intl.cloud.tencent.com/document/product/214/8848).
  - For a bill-by-IP account, the instance fee and public network fee are charged for purchasing a public network CLB instance. For more information, please see [Bill-by-EIP/CLB Account Billing Description](https://intl.cloud.tencent.com/document/product/214/36998).

### Private network CLB
If you need to use CLB to distribute requests from private networks, please select "Private Network".
Both the client and server of private network CLB are in Tencent Cloud and can only be accessed within Tencent Cloud. Access via the internet is not allowed (no public network IP address). Tencent Cloud will assign a private IP to CLB from the network you have selected (such as a [VPC](https://intl.cloud.tencent.com/document/product/215)). The request traffic will be routed to the backend CVM instance via this IP address.
If your application has multiple layers, such as web servers that can communicate over the internet or database servers that can only communicate over the private network, you can create a framework with both public and private network CLB instances. You can then connect all web servers to the public network CLB instance and database servers to the private network CLB instance. The public network CLB instance receives requests from the internet and sends them to the backend web servers. After being processed, requests to database will be sent to the private network CLB instance, which will then route the requests to database servers.
- **Use Cases**
  - Tencent Cloud has more than one internal servers. Requests from the client need to be allocated to servers properly.
  - Fault tolerance and restoration are needed for the internal server cluster.
  - The service provider wants to block their own physical IP addresses and provide imperceptible services to the client.
- **Billing**
   Private network CLB instances are free of charge.

## IP Versions
The IP version of a CLB instance. Available versions: IPv4, IPv6, and IPv6 NAT64.

## Enabling Anycast
If you enable Anycast during the CLB instance creation, an Anycast CLB instance will be created. Anycast CLB is a load balancing service that supports dynamic acceleration across regions. CLB VIP is published in multiple regions. The client connects to the nearest POP, and the traffic will be forwarded to a CVM instance through the high-speed internet of Tencent Cloud IDC. For more information, please see [Creating an Anycast Instance](https://intl.cloud.tencent.com/document/product/214/32426).

## Instance Name
CLB instance name, which can contain 1 to 60 characters.

## Purchase Quantity
Number of purchased CLB instances.
