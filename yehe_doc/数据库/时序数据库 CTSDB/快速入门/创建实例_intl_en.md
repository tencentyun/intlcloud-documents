
This document describes how to purchase a CTSDB instance in the console.

## Prerequisites
You have [signed up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and completed [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
1. Log in at the [CTSDB purchase page](https://buy.intl.cloud.tencent.com/ctsdb), select various configuration items of the database, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: Pay-as-you-go.
 - **Region and AZ**: Select the region where your business needs to be deployed. For more information, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/1100/40937).
 - **Version**: CTSDB 1.0 or CTSDB 2.0.
    - [CTSDB 1.0](https://intl.cloud.tencent.com/document/product/1100/40910) is compatible with Elasticsearch 6.8.2.
    - [CTSDB 2.0](https://intl.cloud.tencent.com/document/product/1100/45526) is compatible with Elasticsearch 7.10.1 and supports SQL-like query statements, data compression algorithms, and write performance optimization; therefore, it is recommended.
 - **Configuration Mode**: Select **QuickConfig** or **CustomConfig**.
 - **Storage Capacity**: In the QuickConfig mode, the storage (i.e., storage capacity per replica) = total disk capacity of the cluster / number of replicas.
 - **Network**: Select the network where the database instance resides. We recommend you select the same VPC in the same region as the CVM instance to be connected to; otherwise, the database instance cannot connect to the CVM instance over the private network. For more information, see [Network Environment](https://intl.cloud.tencent.com/document/product/213/5227).
 - **Port**: Custom ports must fall between 1024 and 65535.
 - **Project**: Select a project to which the instance belongs. The default project is used.
 - **Tag**: Add tags to your instance for easy classification and management. Click <b>Add</b> to select tag keys and values.</td></tr> 
 - **Instance Name**: Name the instance now or later. 
 - **Password**: The root account password must contain 8–64 characters in the following three types: letters, digits, and special symbols `~!@#$%^&*()_+-=|{}[]:;<>,.?/`.
 - **Fees**: For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/1100/40934). 
2. After completing the purchase, return to the instance list. After the status of the instance changes to **Running**, it can be used normally.


## References
[Connecting to Instance](https://intl.cloud.tencent.com/document/product/1100/40928)