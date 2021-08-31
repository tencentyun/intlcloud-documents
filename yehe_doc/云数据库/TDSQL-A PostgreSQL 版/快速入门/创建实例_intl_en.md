
This document describes how to create an instance in the TDSQL-A for PostgreSQL console.
>?TDSQL-A for PostgreSQL is currently in beta test. If you want to try it out, please [submit an application for beta test eligibility](https://cloud.tencent.com/apply/p/vbtsrbx5vd).

## Directions
1. Log in to the [TDSQL-A for PostgreSQL console](https://console.cloud.tencent.com/tdsqla/tdapg) and click **Create** in the instance list.
![](https://main.qcloudimg.com/raw/df2003395468346d1adf8f025ab8d26f.png)
2. Select the region, network, character set, etc., on the purchase page based on your actual business needs and click **Buy Now**.
 - Billing Mode: currently, monthly subscription billing is supported.
 - Region and AZ: we recommend you select the region of your CVM instance, as Tencent Cloud services in different regions cannot interconnect.
 - Network Type: VPC (default). Select the specific VPC and subnet.
    - If needed, you can create a [VPC](https://console.cloud.tencent.com/vpc/vpc?rid=1) and [subnet](https://console.cloud.tencent.com/vpc/subnet?rid=1) in the console.
    - After a VPC is selected, it cannot be changed. For more information on VPC operations, please see [Managing VPC Instances](https://cloud.tencent.com/document/product/215/36515).
 - Security Group: it is left empty by default. If your business requires other ports to be opened, please [customize the security group](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1).
![](https://main.qcloudimg.com/raw/b9ba3a8dde377735bb5ddb9528f8286d.png)
3. After submitting the activation information, return to the instance list. After the status of the instance changes to **Running**, the instance can be connected to.
