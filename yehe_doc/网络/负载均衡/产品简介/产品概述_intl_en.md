## CLB Overview
Tencent Cloud Load Balancer (CLB) is a service that distributes traffic to multiple [CVM](https://intl.cloud.tencent.com/document/product/213/495) instances so as to elevate service capabilities of an application system and eliminate single points of failure for a higher availability.

CLB virtualizes multiple CVM instances **in the same region** into a high-performance and high-availability application service pool by setting a virtual IP address (VIP) and then distributes the network requests from clients to the pool in the manner specified by the application.

CLB checks the health of the instances in the pool and automatically isolates unhealthy ones, solving the problem with single points of failure and improving the service capabilities of the application systematically.

CLB has advanced features such as self-service management, self-healing, and network attack prevention, making it ideal for various application scenarios ranging from business and community to ecommerce and gaming.

## Components
A CLB cluster generally consists of the following components:
- CLB instance: CLB instance used for distributing traffic.
- Virtual IP (VIP): IP address through which CLB provides service to clients.
- Backend/Real server: backend CVM instance used for processing requests.
- VPC/Basic network: overall network environment.

Access requests from outside CLB will be distributed to real servers for processing by the CLB instance based on the configured policy and forwarding rule.

## Glossary

| Term | Meaning | Description |
| ------- | --------------------- | ---------------------------------------- |
| CLB   | Cloud load balancer   | It is a CLB service offered by Tencent Cloud, which provides TCP/UDP- and HTTP-based network load balancing services in conjunction with CVM instances. |
| CLB listener | Load balancer listener | It the listener of a CLB service and consists of listening ports, load balancing policies, and health check configurations, where each listener corresponds to an application service on the backend. |
| RS | Real server | It is a CVM instance that accepts the requests distributed by CLB which forwards the access requests to a set of backend CVM instances for processing according to user-defined rules. |
| VIP | Virtual IP | It is a service address assigned by the system, which currently is an IP address. You can choose whether to open it to the internet so as to create a public or private network CLB instance. |

## How It Works
### Basic principle
A CLB instance receives inbound traffic from clients and routes requests to real servers in one or multiple AZs for processing.

The load balancing service is mainly provided by a CLB listener which listens on the CLB instance for requests and executes corresponding policies to distribute requests to services such as real servers. You can configure the forwarding protocol and protocol port in **client - CLB** and **CLB - real server** dimensions to have CLB directly forward requests to real servers.

You are recommended to configure backend CVM instances in multiple AZs for a CLB instance. In this way, if one AZ becomes unavailable, the CLB instance will route the traffic to other normal instances in other AZs so as to avoid service interruption caused by AZ failure.

### Selecting request route
A client request accesses the service through a domain name. Before a request is sent to a CLB instance, the DNS server will resolve the CLB domain name and return to the client the CLB IP address that receives the request. When the CLB listener receives requests, it will use different CLB algorithms to distribute them to real servers. Currently, Tencent Cloud supports multiple load balancing algorithms such as WRR, ip_hash, and weighted least-connection scheduling.

### Monitoring real server status
A CLB instance can monitor the running status of real servers to ensure that traffic is routed to only healthy servers. When the CLB instance detects that a real server is exceptional, it will stop routing traffic to the server and resume routing after detecting that the server runs normally again.

## Related Services
CLB can be used together with the following services to improve the availability and scalability of applications:
- [CVM](https://intl.cloud.tencent.com/document/product/213) instance: it is a virtual server for applications to run in the cloud.
- [Auto Scaling](https://intl.cloud.tencent.com/document/product/377): it automatically controls the instance quantity. If CLB instances are enabled in Auto Scaling, instances scaled out will be automatically added to the CLB cluster, while instances scaled in will be automatically removed from the cluster.
- [Cloud Monitor](https://intl.cloud.tencent.com/document/product/248): it helps you monitor running status of CLB instances and all real servers and allows you to perform relevant operations.
