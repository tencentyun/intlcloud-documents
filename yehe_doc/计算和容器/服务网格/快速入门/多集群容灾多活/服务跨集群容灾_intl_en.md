

 ## Overview
 This document describes how to implement disaster recovery capabilities across regions (AZs) for all services. In this way, when a service in a region (AZ) fails, traffic to the service will be automatically switched to another region (AZ).
Cross-region service disaster recovery is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3a0c2aaab973912383c5bf1d6a316dbc.png)

## Verification
By default, Tencent Cloud Mesh provides cross-region (AZ) service disaster recovery capabilities, as verified below.

To begin with, set the number of Pods in the `product-v2` Deployment of the primary cluster to `0` in the TKE console. This is to simulate product service failures in the AZ of the primary cluster.
Adjust the number of Pods as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/af44b95dd04cc855438c291dee10d45a.png)


After the configuration, access the demo ecommerce website through the IP address of the edge gateway of the primary cluster. Even if the product service in AZ A of the primary cluster fails, you can still access the product page and view service calls in the floating window in the bottom-left corner. The current page calls the product service in another AZ, indicating that access requests to the product service in AZ A are routed to the product service in AZ B, implementing cross-AZ disaster recovery at the service level.

Deploy two clusters in different regions to implement cross-region disaster recovery at the service level.
Cross-AZ disaster recovery of the product service is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/fe7644d7481da15e8830481fdb5ec1c3.png)