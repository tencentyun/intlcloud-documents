CLB is mainly suitable for the following scenarios:
- Traffic distribution. CLB can distribute the traffic of business with a large number of access requests to multiple CVM instances.
- Elimination of single point of failure. When some CVM instances become unavailable, CLB can automatically block them to ensure the normal operation of the application system.
- Horizontal scalability. You can scale out the service capability of application systems as needed, which is suitable for web and app servers.
- Global load balancing. CLB supports global multi-region load balancing to ensure remote disaster recovery.

## Traffic Distribution and Elimination of Single Point of Failure
You can use CLB to distribute business traffic to multiple CVM instances.
- Business client accesses CLB.
- Multiple CVM instances form a high-performance and high-availability service pool, to which CLB forwards the business traffic.
- When one or more CVM instances become unavailable, CLB can automatically block them and distribute the requests to normal CVM instances, ensuring the operation of the application system.
- If your business is deployed in multiple availability zones, it is recommended that you bind a CLB instance to CVM instances in multiple availability zones at the same time to ensure multi-availability zone disaster recovery at the real server layer.
- The session persistence feature can forward requests from the same client to the same real server, improving access efficiency.
![](https://qcloudimg.tencent-cloud.cn/raw/af522691e22caa4cc6160a7fe17880d8.svg)

## Horizontal Scalability
With [Auto Scaling](https://intl.cloud.tencent.com/document/product/377), CLB can automatically create and release CVM instances based on your business needs.
- You can configure auto scaling policies to manage the number of CVM instances, deploy the instance environment, and ensure the operation of your business. CLB can automatically add CVM instances when demands peak to keep high performance, while removing CVM instances when demands drop to reduce costs.
- For example, during major sales campaigns in ecommerce such as Black Friday, web traffic may suddenly increase by 10 times and lasts only for a few hours. In this case, CLB and AS can be used to maximize IT cost savings.
![](https://qcloudimg.tencent-cloud.cn/raw/38d3f5c690ecb3344e75af20431d5986.svg)

## Global Load Balancing
Combined with DNSPod, CLB enables you to resolve business traffic to the global load balancing in various regions, ensuring remote multi-site active-active and disaster recovery.
- You can deploy CLB instances in different regions and bind them to CVM instances in corresponding regions.
- You can use DNSPod to resolve domain names to CLB VIPs in various regions.
- Business traffic will be forwarded to multiple CVM instances in multiple regions via DNS and CLB, achieving global load balancing.
- When a region becomes unavailable, you can suspend resolution of the CLB VIP in that region to ensure that your business is not affected.
![](https://qcloudimg.tencent-cloud.cn/raw/5a71a839a2aa222e16b878e28c26c7db.svg)


