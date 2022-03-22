
This document describes how to create a cluster in the TDSQL-C console.

## Prerequisites
To purchase instances, you need to verify your identity first. For more information, see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [TDSQL-C purchase page](https://buy.intl.cloud.tencent.com/cynosdb?regionId=8), select the deployment region, AZ, database specification, and other information, and click **Buy Now**.
 - **Billing Mode**: monthly subscription, pay-as-you-go, and serverless billing modes are supported.
 - **Network**: for performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C clusters only in the same [VPC](https://intl.cloud.tencent.com/document/product/215).
 - **Compatible Database**: MySQL 5.7 and 8.0 and PostgreSQL 10 are supported.
 - **Compute Instance Quantity**: we recommend you select at least two instances to ensure the high availability of the cluster. After the cluster is created, you can expand its read capacity by adding read-only instances.
 - **Instance Specification**: for more information on the database specifications and prices, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620).
 - **Storage billing**:
    - Pay-as-You-Go billing is supported, that is, you don't need to specify a storage option at the time of purchase. TDSQL-C is billed by the actual storage usage per hour.
    - Monthly subscription billing is supported, that is, you purchase monthly-subscribed storage space now (billed in the entirety regardless of whether it is used up).
>?Only TDSQL-C for MySQL supports the purchase of monthly-subscribed storage space under the premise that you select the monthly subscription billing mode.
![](https://qcloudimg.tencent-cloud.cn/raw/2f20264b2680a4268de1a034c3184566.png)
 - **Project**: select a project to which the database belongs. The default project is used.
 - **Quantity**: you can purchase up to 10 pay-as-you-go TDSQL-C clusters in each AZ.
>?When the amount of data stored in a cluster exceeds its maximum storage space, the cluster can only read but not write data. In this case, you can choose to delete redundant data or upgrade the specification.
>
2. After the purchase is completed, you will be redirected to the cluster list. After the status of the cluster becomes **Running**, it can be used normally.

## Subsequent Operations
After purchasing the TDSQL-C cluster, you can connect to it through its private or public network address or DMC. For more information, see [Connecting to TDSQL-C Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).
