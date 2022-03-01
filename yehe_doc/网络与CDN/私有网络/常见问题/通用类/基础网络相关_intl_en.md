>? Tencent Cloud plans to discontinue the service of classic network. Staring from **January 31, 2022**, no more new resource can be created on the classic network. The classic network service will be officially discontinued on **December 31, 2022**. After that, all classic network-based resources will be migrated to VPC.
>

### Are my resources running on the classic network still available after January 31, 2022?
Your existing resources running on the classic network are still available till **December 31, 2022**. We recommend you migrate your resources to  a VPC as soon ass possible. For more information, see [Migration Solutions](https://intl.cloud.tencent.com/document/product/215/38117).

### Will my business be interrupted during the migration from the classic network to VPC?
This depends on the specific Tencent Cloud service that you use:
+ For TencentDB services, your services are not affected as dual-IP accessing is supported during migration.
+ To migration a CVM instance, the instance must be shut down, which will interrupt your service for a shor while. We recommend you migrate during off-peak hours.
+ CLB 不支持直接迁移，可重建相同配置的实例，将业务流量逐步迁移。

### Will the billing mode change after the migration from the classic network to VPC?
The billing mode is not changed.

### Will the original private IP of the instance change after the migration from the classic network to VPC?
If the IP of the instance is within the target VPC IP range, you can keep the private IP unchanged by specifying it as the new IP. Otherwise, the IP will change.

### Will the original public IP of the instance change after the migration from the classic network to VPC?
The original public IP will remain the same.

### Can I migrate a CVM from a VPC to the classic network?
No. 



### What are the differences between the classic network and VPC?
基础网络与私有网络均为云上网络空间，区别在于：
- The classic network is a public network resource pool shared by all Tencent Cloud users. The private IPs of all CVMs are assigned by Tencent Cloud. You cannot customize IP ranges or IP addresses.
- A VPC is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies, making it more suitable for use cases requiring custom configurations.

### What are the strengths of a VPC?
- It allows you to customize IP ranges, IP addresses, and routing policies.
- It supports more complex scenarios such as ENI, network ACL, and cross-region communication.
- It improves the disaster recovery capability and availability greatly.

### Can I migrate a CVM from the classic network to a VPC? 
Yes. You can migrate CVMs from the classic network to a VPC. See [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
>!This operation cannot be undone. Be sure to carefully read the document before performing this operation.



### Which Tencent Cloud products support the classic network?
- Classic network servers: CVM, GPU Cloud Computing, and FPGA Cloud Computing.
- Classic network database: TencentDB for MySQL, Redis, SQL Server, PostgreSQL, and MongoDB, as well as TDSQL for MySQL.
- Classic network load balancer: classic CLB and CLB
- Others: classic network CFS and classic network CKafka.

### How can I establish communication between a classic network-based CVM and a VPC-based CVM?
You can use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) to establish communication between the classic network and VPCs.
Note the following limitations when using Classiclink:
1. Both the classic network and the VPC to be communicated with are located in the same region (they can be in different availability zones, such as Guangzhou Zone 1 and Guangzhou Zone 2).
2. The VPC CIDR block (IP range) must fall within `10.[0-47].0.0/16` (including subsets). Otherwise, there will be conflicts.

If these conditions are met, you can configure Classiclink on the VPC details page in the console, to associate the classic network-based CVMs with the VPC for interconnection.

### Can resources such as cloud load balancers and databases in the classic network communicate with the VPC?
- A terminal connection helps instances in a VPC to communicate with instances in the classic network instances through a private network. It maps classic network instance IPs to VPC IP addresses, allowing you to access the classic network instances through the VPC IPs. Classic network products that support terminal connections include CLB, TencentDB, CMEM, Redis, and MongoDB. However, cross-region or cross-account communication is not supported.
- Direction: one-way (the VPC accesses the classic network).
- If needed, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Can the classic network and VPC instances under different accounts communicate with each other?
No. A VPC supports more features with greater flexibility, and therefore we recommend that you migrate resources from the classic network to a VPC.

### How can I disassociate a VPC from a CVM in the classic network?
您好，解关联步骤如下：
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc).
2. Click the **ID/Name** of the VPC which needs Classiclink to access the details page.
3. Click **Classiclink**. Select the classic network-based CVM to be disassociated and click **Disassociate**.
4. Click **OK**.

For step-by-step instructions, see [Classiclink Overview](https://intl.cloud.tencent.com/document/product/215/31807).
