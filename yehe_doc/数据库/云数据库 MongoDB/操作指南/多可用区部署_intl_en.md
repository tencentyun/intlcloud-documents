Multi-AZ deployment refers to deployment of TencentDB for MongoDB replicas across multiple AZs in the same region. Multi-AZ deployed instances have higher availability and better disaster recovery capability than single-AZ deployed instances.

## Creating Multi-AZ Deployed Instance
1. Log in to the [TencentDB for MongoDB purchase page](https://buy.intl.cloud.tencent.com/mongodb) with a Tencent Cloud account.
2. On the purchase page, configure the multi-AZ deployment parameters.
![](https://qcloudimg.tencent-cloud.cn/raw/0ac0500f3d5d7122c887a581f98d0e50.png)
  - In the **Billing Mode** field, select a billing mode as needed. **Pay-as-you-go** is supported. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/240/3550).
  - In the **Region** field, select the region of the multi-AZ deployed instance. We recommend you select the region closest to your end users to minimize the access latency.
  - In the **AZ** field, you can click **Multi-AZ Deployment** and select the AZ in the drop-down lists after **Primary Node**, **Secondary Node 1**, and **Secondary Node 2** respectively. To guarantee a smooth cross-AZ switch, multi-AZ deployment does not support deploying most cluster nodes in the same AZ; that is, the primary and secondary nodes can be deployed only in three different AZs separately.
  - For more information on how to configure other parameters, see [Creating TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/3551).
3. Click **Billing Details** to view product pricing and confirm the total fees.
4. Click **Buy Now**. After the purchase success message is displayed, click **Go to Console** to enter the instance list page. After the instance status in the **Monitoring/Status** column becomes **Running**, the multiple AZs of the instance will be displayed in the **AZ** column.

## Accessing Multi-AZ Deployed Instance
You can use MongoDB Shell or a concatenated URI through the SDK client for multiple programming languages to access a multi-AZ deployed instance. For detailed directions, see [Connecting to TencentDB for MongoDB Instance](https://intl.cloud.tencent.com/document/product/240/7092).

## Upgrading from Single-AZ to Multi-AZ Deployed Instance
You can upgrade a single-AZ deployed instance to a multi-AZ deployed instance. For detailed directions, see [Modifying Instance AZ](https://intl.cloud.tencent.com/document/product/240/44182).

