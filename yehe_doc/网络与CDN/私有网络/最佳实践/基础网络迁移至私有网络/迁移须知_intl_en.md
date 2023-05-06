The classic network is an earlier cloud network provided by Tencent Cloud. As the user scale and services expand, Virtual Private Cloud (VPC) evolves from the classic network to provide independent, controllable, and more secure networks. As a mainstream cloud network, VPC provides better user experience. This document provides answers to questions that you may have when you migrate resources from the classic network to VPC.

## Why Do I Need to Migrate Resources to VPC?
A VPC is a logically isolated network space in Tencent Cloud and has the following advantages:
+ It allows you to customize IP ranges, IP addresses, and routing policies.
+ It supports more complex scenarios such as Elastic Network Interface (ENI), network access control list (ACL), and cross-region communication.
+ It improves the disaster recovery capability and availability greatly.
+ It supports multiple Cloud Virtual Machine (CVM) models.

VPC is more suitable for use cases that require custom configurations compared with the classic network. To provide you with better services, Tencent Cloud will fully upgrade the classic network. From **March 31, 2022**, resources cannot be created on the classic network. Services on the classic network are officially discontinued on **December 31, 2022**. These services are replaced with the corresponding VPC services.

## Is My Business Running on the Classic Network Affected After March 31, 2022?
Your existing resources running on the classic network are still available until **December 31, 2022**. We recommend you migrate your resources to VPC as soon as possible.

## What Is the Impact If I Do Not Migrate Resources to VPC?
Before the classic network is discontinued, your existing resources will not be affected. After the classic network is discontinued, the services of the classic network will no longer be available. Therefore, we recommend you migrate your resources to VPC before **December 31, 2022**.  

## How Do I Determine Whether I Need to Migrate Resources to VPC?
1. Check whether your account is created before **00:00 June 13, 2017**. If your account is created after 00:00 June 13, 2017, the classic network is not supported for your account and the cloud resources that you purchase are already in VPC. In this case, you do not need to migrate resources to VPC. If your account is created before 00:00 June 13, 2017, go to Step 2.
2. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), choose **Fees** > **My Orders**, and check whether you have purchased the following resources:
  
 + Classic network servers: CVM, GPU Cloud Computing, and FPGA Cloud Computing.
 + Classic network databases: TencentDB for MySQL, Redis, SQL Server, PostgreSQL, and MongoDB, as well as TDSQL for MySQL.
 + Classic network load balancers: classic Cloud Load Balancer (CLB) and CLB.
 + Others: classic network Cloud File Storage (CFS) and classic network Cloud Kafka (CKafka).
>? Lighthouse is not a service of the classic network, but a VPC service. Therefore, it does not require migration.
>
3. If you have purchased any of the preceding resources, log in to the console for each resource and check whether the network attribute of the resource is classic network. If not, ignore the network migration notice.
Take CVM as an example. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance/index?rid=1) and check the network attribute of each CVM instance. If the network attribute is **classic network**, you need to perform network migration. If the network attribute is **VPC**, ignore the network migration notice.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HhC2958_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230406181041.png)
>? If you have purchased many resources, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
>

## Will the Billing Mode of an Instance Change After the Migration from the Classic Network to VPC?
The billing mode is not changed.

## Will the Configuration of an Instance Change After the Migration from the Classic Network to VPC?
+ The public IP remains unchanged, and the instance can still be accessed by using the original domain name.
+ The Media Access Control (MAC) address remains unchanged, but the private IP will be changed.
>? If the IP of the instance is within the target VPC IP range, you can keep the private IP unchanged by specifying it as the new IP. Otherwise, the private IP will change.
>

## Will the Services Be Interrupted During the Migration from the Classic Network to VPC?
This depends on the specific Tencent Cloud service that you use:
+ During the migration of a CVM instance, the instance must be restarted, which will interrupt your service for a short while. We recommend you migrate the instance during off-peak hours.
+ For TencentDB services, your services are not affected as dual-IP accessing is supported during migration.
+ CLB doesn't support direct migration. You can rebuild instances with the same configuration and gradually migrate the business traffic.

## Can I Migrate an Instance Back to the Classic Network?
No, you cannot migrate an instance back to the classic network after it is migrated to VPC.

## Can I Migrate a Classic Network Instance in a Region to a VPC Instance in Another Region?
No, instances can be migrated only to the same region and availability zone.

## Is Network Migration Implemented by Tencent Cloud?
No, you need to manually perform the migration. If you have any questions, [submit a ticket](https://console.cloud.tencent.com/workorder/category). 
