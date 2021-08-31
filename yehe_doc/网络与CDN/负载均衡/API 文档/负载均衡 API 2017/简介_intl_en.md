Welcome to Tencent Cloud Load Balancer. Cloud Load Balancer (CLB) sends the requests from client to multiple associated backend [CVMs](https://intl.cloud.tencent.com/document/product/213/495) in the same region with the specified method by setting a virtual IP (VIP).

CLB virtualizes multiple CVMs into an available application service pool. It checks the health of the instances in the pool and automatically isolates the unhealthy ones, thus resolving single points of failure issues and improving the overall service capabilities of the applications. In addition, CLB provides a defense capability of more than 300 Gbit/sec against DDoS attacks.

CLB is a solution that serves multiple machines simultaneously, and it must be used together with CVM. **The APIs in this document help you operate on CLB instances. Before using these APIs, please ensure that you are familiar with [overview](https://intl.cloud.tencent.com/document/product/214/524) and [use](https://intl.cloud.tencent.com/document/product/214) of CLB.**


## Glossary

| Term | Full Name | Description |
|---------|---------|---------|-----|
| CLB | Cloud Load Balancer | Cloud Load Balancer sends the requests from client to the associated CVMs in the same region with specified method by setting a virtual IP (VIP). It can automatically isolate unhealthy CVMs, thus resolving single points of failure and massive concurrent access requests issues. |
| Listener | Load Balancer Listener| CLB listener provides users with customized listening port, request forwarding policy, health check configuration, etc. |
| backend | Real Server | A CLB instance sends requests to real servers which will provide service in a real sense. |
| VIP | Virtual IP | A CLB instance provides the virtual IP of service. |

## How to Use
Before using CLB through APIs, please make sure that a port is open on one or more CVMs, e.g. TCP port 80. Next, you need to perform the following steps:
1. Purchase a CLB instance.
You can create a CLB instance using the [CreateLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1254) API, and obtain the unique ID of this instance.
2. Create a CLB listener.
After purchasing a CLB instance, you need to use the [CreateLoadBalancerListeners](https://intl.cloud.tencent.com/document/product/214/1255) API to create a listener that listens on a protocol and port. For example, you can create a TCP listener that listens on TCP port 80 and backend port 80.
3. Bind the real server to the CLB instance.
Finally, you need to bind the CVM on which the service is deployed to the CLB instance through the [RegisterInstancesWithLoadBalancer](https://intl.cloud.tencent.com/document/product/214/1265) API.

After performing these three steps, you can access the service deployed on your CVM by accessing the VIP and port of the CLB instance.
