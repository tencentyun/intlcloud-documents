## What is Cloud Load Balancer?
Cloud Load Balancer (CLB) is a service that distributes traffic to multiple CVMs. CLB expands the external service capabilities of the application system through traffic distribution and improves the availability of the application system by eliminating single-point failures. For information on CVM, see [CVM Overview](https://intl.cloud.tencent.com/document/product/213/495).

CLB virtualizes multiple CVM instances **in the same region** into a high-performance and high-availability application service pool by setting a virtual IP address (VIP) and then distributes the network requests from clients to the pool in the manner specified by the application.

CLB checks the health of the instances in the pool and automatically isolates unhealthy ones, thus resolving single points of failure issues and improving the overall service capabilities of the applications.

Tencent CLB, featuring self-service management, self-service fault repair, and defense against network attacks, is applicable for application scenarios such as enterprises, communities, e-commerce, and games.

## Components
A working CLB group usually consists of the following components:
- **Cloud Load Balancer**: A CLB instance used for traffic distribution.
- **VIP (virtual IP)**: The IP address used for the CLB to provide service to clients.
- **Backend/Real Server**: A set of CVM instances in the backend used for processing requests.
- **VPC/Classic Network**: Overall network environment.

The access requests from outside the CLB are distributed to the backend CVMs based on policies and forwarding rules for processing through the CLB instance.

## Glossary
<table>
<tr>
<th width="19%">Term</th>
<th width="15%">Full Name</th>
<th width="66%">Description</th>
</tr>
<tr>
<td>CLB</td>
<td>Cloud Load Balancer</td>
<td>A network load balancing service provided by Tencent Cloud, which can be combined with CVM to provide users with TCP/UDP- and HTTP-based load balancing services.</td>
</tr>
<tr>
<td>CLB Listener</td>
<td>Cloud Load Balance Listener</td>
<td>Includes listening port, load balancing policy and health check configuration, each of them corresponds to an application service in the backend. </td>
</tr>
<tr>
<td>Backend CVM</td>
<td>Real Server</td>
<td>A group of CVM instances that receive the requests forwarded by the CLB according to the rules set by the users.</td>
</tr>
<tr>
<td>Virtual Service Address</td>
<td>Virtual IP</td>
<td>The service address (currently the IP address) assigned by the system. Users can choose whether to disclose the service address to create public/private network-based load balancing services. <ul><li>Public network VIP<ul><li>Regular IP: Common BGP IP, used to balance network quality and cost.</li><li>Accelerated IP: Accelerated by using Anycast to make public network access more stable, reliable and low-latency.</li><li>Static single-line IP: Accesses the public network through a single ISP, which is low-cost and convenient for autonomous scheduling.</li></ul></li><li>Private network VIP<ul><li>VPC: IP within the VPC.</li><li>Classic network: Private IP of the classic network.</li></ul></li></ul></td>
</tr>
</table>

## How it Works
### Basic Working Principle
A CLB instance receives inboud traffic from clients and routes requests to backend CVMs in one or more availability zones for processing.

The CLB service works primarily by the load balancing listener. The listener monitors the requests on the CLB instance and distributes them to the backend CVMs by executing policies. The CLB can forward the requests to the backend CVMs directly by configuring the forwarding protocols and protocol ports on the two dimensions:**Client - CLB** and **CLB - Backend CVM**.

It is recommended that you configure the backend CVM instances across multiple availability zones for the CLB. This enables CLB to route traffic to CVM instances running normally in other availability zones when one availability zone is unavailable, thereby avoiding service interruptions caused by availability zone failures.

### Request Routing
The client requests to access the service through the domain name. Before the request is sent to the load balancer, the DNS server resolves the CLB domain name and returns the requested CLB IPs to the client. When the CLB listener receives a request, it uses different load balancing algorithms to distribute the request to the backend CVMs. Tencent Cloud currently supports multiple balancing algorithms including weighted round robin and `ip_hash` weighted minimum connections.

### Backend CVM Monitoring
A load balancer can also monitor the running status of backend CVMs to ensure that traffic is only routed to the normally running CVMs. The load balancer will stop routing traffic to an abnormal CVM and reroute traffic to it when it is running normally again.

## Additional Services
CLB works with the following services to improve application availability and scalability:
- [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213) Instance: A virtual server where the application runs on the cloud.
- [Auto Scaling](https://intl.cloud.tencent.com/document/product/377): Controls the instance number elstically. If a CLB is enabled in auto scaling, the scaled instance is automatically added to the CLB group, and the terminated instance is automatically removed from the CLB group.
- [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248): Helps you monitor the CLB and the running status of all backend CVM instances and perform required operations.


