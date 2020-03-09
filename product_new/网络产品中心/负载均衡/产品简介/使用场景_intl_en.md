CLB is mainly suitable for the following scenarios:
- Traffic distribution. CLB can distribute the traffic of business with a large number of access requests to multiple CVM instances.
- Elimination of single point of failure. When some CVM instances become unavailable, CLB can automatically block them to ensure the normal operation of the application system.
- Horizontal scalability. You can scale out the service capability of application systems as needed, which is suitable for web and app servers.
- Global load balancing. With Tencent Cloud DNS, CLB can support global and multi-regional load balancing for remote disaster recovery.

## Traffic distribution and elimination of single point of failure
You can use CLB to distribute business traffic to multiple CVM instances.
- Business client accesses CLB.
- Multiple CVM instances form a high-performance and high-availability service pool, to which CLB forwards the business traffic.
- When one or more CVM instances become unavailable, CLB can automatically block them and distribute the requests to normal CVM instances, ensuring the operation of the application system.
- The session persistence feature can forward requests from the same client to the same real server, improving access efficiency.

## Horizontal Scalability
With [Auto Scaling (AS)](https://intl.cloud.tencent.com/document/product/377), CLB can automatically create and release CVM instances based on your business needs.
- You can configure auto scaling policies to manage the number of CVM instances, deploy the instance environment, and ensure the operation of your business. CLB can automatically add CVM instances when demands peak to keep high performance, while removing CVM instances when demands drop to reduce costs.
- For example, during major sales campaigns in ecommerce such as Black Friday, web traffic may suddenly increase by 10 times and lasts only for a few hours. In this case, CLB and AS can be used to maximize IT cost savings.

## Global Load Balancing
With Tencent Cloud DNS, you can resolve your business traffic to global and multi-regional CLB instances to implement active-active and remote disaster recovery acorss regions.
- You can deploy CLB instances in different regions and bind them to CVM instances in corresponding regions.
- You can use Tencent Cloud DNS to resolve domain names to the CLB VIP in each region.
- Business traffic will be forwarded to multiple CVM instances in multiple regions via DNS and CLB, achieving global load balancing.
- When a region becomes unavailable, you can suspend resolution of the CLB VIP in that region to ensure that your business is not affected.
