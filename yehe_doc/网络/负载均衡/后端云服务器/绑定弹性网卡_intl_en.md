## ENI Overview
[Elastic Network Interface (ENI)](https://intl.cloud.tencent.com/document/product/576/18525) refers to the type of virtual network interfaces that can be bound to CVM instances in VPCs. An ENI can be migrated freely between CVM instances within the same VPC and AZ, helping you easily build high-availability clusters, implement low-cost failover, and manage networks in a more refined manner.
CLB real servers can be bound to both CVM and ENI. Specifically, a CLB instance communicates with the real server over the private network, and if multiple CVM instances and ENIs are bound to the CLB instance, access traffic will be forwarded to the private IPs of the CVM instances and ENIs.
> The ENI binding feature of CLB is currently in beta test. If you want to use it, please [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=163&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%20LB) for application.

## Prerequisites
An ENI must be bound to a CVM instance first before it can be bound to a CLB instance. As a CLB instance only forwards traffic as a load balancer but does not process the business logic, the CVM instance, as a computing resource, is needed to process user requests. Please log in to the [ENI Console](https://console.cloud.tencent.com/vpc/eni) to bind the required ENI to the CVM instance first.
![](https://main.qcloudimg.com/raw/3d7c79999350a4b80e0a2b2f546b559f.png)

## Directions
1. You need to configure a CLB listener first. For more information, please see [CLB Listener Overview](https://intl.cloud.tencent.com/document/product/214/6151).
2. Click **+** on the left of the created listener to expand the domain names and URL paths, select the desired URL path, and view the existing real server bound on the right of the listener.
![](https://main.qcloudimg.com/raw/0c0ed8c9e456cfb52126f34537f0f779.png)
3. Click **Bind** and select the real server to be bound and configure the server port and weight in the pop-up window. You can select "CVM" or "ENI" as the real server.
 - CVM: you can bind the primary private IPs of primary ENIs of all CVM instances in the same VPC as the CLB instance.
 - ENI: you can bind all ENI IPs in the same VPC as the CLB instance except the primary private IPs of primary ENIs of CVM instances, such as secondary private IPs of primary ENIs and private IPs of secondary ENIs. For more information on the types of ENI IPs, please see [ENI - Key Concepts](https://intl.cloud.tencent.com/document/product/576/18526). 
![](https://main.qcloudimg.com/raw/89fdb725e535b81361d9a80ab0984e7a.png)
4. The specific configuration after binding is as shown below:
![](https://main.qcloudimg.com/raw/46defc2ad3e445e4acd6808c22aeb937.png)
