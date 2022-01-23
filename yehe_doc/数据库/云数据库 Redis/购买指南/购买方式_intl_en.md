
TencentDB for Redis can be purchased in the console or through an API.

## Purchasing Instances in the Console
1. Log in to the [TencentDB for Redis purchase page](https://buy.intl.cloud.tencent.com/redis), configure the following instance information, confirm that everything is correct, and click **Buy Now**.
  - **Billing Mode**: pay-as-you-go
    - If the request volume of your business fluctuates greatly and instantaneously, we recommend you choose pay-as-you-go billing.
 - **Region**: select the region that you want your TencentDB for Redis instance to be deployed in. We recommend that you use the same region as the CVM instance to be connected to. Tencent Cloud products in different regions cannot communicate with each other over the private network. The region cannot be modified after purchase.
 - **Instance Edition**: Memory Edition is supported. It is a high-performance edition based on the open-source Redis engine, which is compatible with Redis v2.8, v4.0, and v5.0.
 - **Compatible Version**: TencentDB for Redis is compatible with Redis v2.8, v4.0, and v5.0. v2.8 is unavailable currently, and v4.0 or later is recommended. To purchase v2.8, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
 -**Architecture**: standard architecture or cluster architecture
 -**Replica Quantity**: TencentDB for Redis v2.8 (Standard Architecture) supports 0 or 1 replica; v4.0 or v5.0 (Standard or Cluster Architecture) supports 1 to 5 replicas.
  - **Network**: select the network where the TencentDB for Redis instance resides. We recommend that you select the same [VPC](https://intl.cloud.tencent.com/document/product/215) in the same region as the CVM instance to be connected to. After the TencentDB instance is purchased, you can switch its network from classic network to VPC, but you cannot switch from VPC to classic network.
 - **Availability Zone**: select availability zones for the master node and replica nodes. Multi-AZ deployed instances have higher availability and better disaster recovery capability than single-AZ deployed instances. For more information, see [Multi-AZ Deployment](https://intl.cloud.tencent.com/document/product/239/39812).
 - **Port**: custom ports must fall between 1024 and 65535.
 - **Parameter Template**: apply a parameter template to configure parameters in batches. For more information, see [Using Parameter Templates](https://intl.cloud.tencent.com/document/product/239/41810).
 - **Project** and **Security Group**: specify a project and [security groups](https://intl.cloud.tencent.com/document/product/239/31945).
 - **Instance Name** and **Set Password**: set the instance name and password here or set them in the instance list after creation.
2. After the purchase is completed, you will be redirected to the instance list. After the status of the read-only replica is displayed as **Running**, it can be used normally.
3. (Optional) Click the **Edit** icon in the **Instance ID/Name** column in the instance list to rename the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/a73ef77b663048109c3fffc74eb01391.png)

## Purchasing Instances via an API
For more information on how to purchase TencentDB for Redis instances via an API, see [CreateInstances](https://intl.cloud.tencent.com/document/product/239/32069).

