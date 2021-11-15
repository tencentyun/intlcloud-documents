
This document describes how to create a cluster in the TDSQL-C console.

## Prerequisites
To make a purchase, you need to complete identity verification first. For more information, please see [Identity Verification Guide](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in to the [TDSQL-C purchase page](https://buy.cloud.tencent.com/cynosdb?regionId=8), select the deployment region, AZ, database specification, and other information, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go and serverless billing modes are supported.
 - **Network**: for performance and security considerations, only VPC network is supported currently. CVM instances can communicate with TDSQL-C clusters only in the same VPC.
 - **Compatible Database**: MySQL 5.7 and PostgreSQL 10 are supported.
 - **Instance Specification**: for more information on the database specifications and prices, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/1098/40620).
 - **Storage Billing**: you don't need to specify a storage option at the time of purchase. TDSQL-C is billed by the actual storage usage per hour.
 - **Project**: select a project to which the database belongs. The default project is used by default.
 - **Quantity**: you can purchase up to 10 pay-as-you-go TDSQL-C clusters in each AZ.
>?When the amount of data stored in a cluster exceeds its maximum storage space, the cluster can only read but not write data. In this case, you can choose to delete redundant data or upgrade the specification.
>
2. After the purchase is completed, you will be redirected to the cluster list. After the status of the cluster becomes **Running**, it can be used normally.

## Subsequent Operations
After purchasing the TDSQL-C cluster, you can connect to it through its private or public network address or DMC. For more information, please see [Connecting to TDSQL-C Cluster](https://intl.cloud.tencent.com/document/product/1098/40627).
