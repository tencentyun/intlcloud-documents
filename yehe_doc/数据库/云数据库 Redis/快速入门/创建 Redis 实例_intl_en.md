
This document describes how to create an instance in the TencentDB for Redis console.

## Prerequisites
You have registered a Tencent Cloud account and completed identity verification.
- To register a Tencent Cloud account:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Click here to sign up for a Tencent Cloud account</a></div>

- To verify your identity:
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Click here to verify your identity</a></div>

## Directions
1. Log in to the [TencentDB for Redis purchase page](https://buy.intl.cloud.tencent.com/redis), configure the following instance information, confirm that everything is correct, and click **Buy Now**.
  - **Billing Mode**: Pay-as-you-go.
 - **Region**: Select the region that you want your TencentDB for Redis instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Instance Edition**: Memory Edition is supported. It is a high-performance edition based on the open-source Redis engine, which is compatible with Redis v2.8, v4.0, and v5.0.
 - **Compatible Version**: TencentDB for Redis is compatible with Redis v2.8, v4.0, and v5.0. v2.8 is unavailable currently, and v4.0 or later is recommended. To purchase v2.8, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
 - **Architecture**: v4.0 or higher supports the standard architecture and cluster architecture, while v2.8 only supports the standard architecture.
 - **Memory**: The optional memory of a single node ranges from 256 MB to 64 GB.
 -**Replica Quantity**: TencentDB for Redis v2.8 (standard architecture) supports zero or one replica; v4.0 or v5.0 (standard or cluster architecture) supports one to five replicas.
 - **Read-Only Replica**: v4.0 or higher supports read-only replicas.
  - **Network**: Select the network where the TencentDB for Redis instance resides. We recommend that you select the same [VPC](https://intl.cloud.tencent.com/document/product/215) in the same region as the CVM instance to be connected to. After the TencentDB instance is purchased, you can switch its network from classic network to VPC, but you cannot switch from VPC to classic network.
 - **Availability Zone**: Select availability zones for the master node and replica nodes. Multi-AZ deployed instances have higher availability and better disaster recovery capability than single-AZ deployed instances. For more information, see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39812).
 - **Port**: Custom ports must fall between 1024 and 65535.
 - **Parameter Template**: Apply a parameter template to configure parameters in batches. For more information, see [Using Parameter Templates](https://intl.cloud.tencent.com/document/product/239/41810).
 - **Project** and **Security Group**: Specify a project and [security groups](https://intl.cloud.tencent.com/document/product/239/31945).
 - **Tag**: You can create tags to manage instance resources.
 - **Security Group**: When creating an instance, you can select an existing security group.
 - **Instance Name** and **Set Password**: Set the instance name and password here or set them in the instance list after creation.
2. After the purchase is completed, you will be redirected to the instance list. After the status of the read-only replica is displayed as **Running**, it can be used normally.
3. (Optional) Click the **Edit** icon in the **Instance ID/Name** column in the instance list to rename the instance.
![](https://main.qcloudimg.com/raw/8a6917c05adb4e06731dbdd836c620da.png)

## Subsequent Operations
- Use a CVM instance to directly access the private IP of the TencentDB instance. For more information, see [Connecting to TencentDB for Redis Instance (over Private Network)](https://intl.cloud.tencent.com/document/product/239/9897).
- Use a CVM instance with a public IP to connect to the TencentDB instance over the public network through port forwarding. For more information, see [Connecting to TencentDB for Redis Instances (over Public Network)](https://intl.cloud.tencent.com/document/product/239/35905).
