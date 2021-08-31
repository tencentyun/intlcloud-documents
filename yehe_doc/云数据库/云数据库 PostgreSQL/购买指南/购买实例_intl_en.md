## Overview
This document describes how to create a database instance in the TencentDB for PostgreSQL console.

## Prerequisites
You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register) and completed [identity verification](https://console.cloud.tencent.com/developer). To purchase TencentDB for PostgreSQL instances in the Chinese mainland, please verify your identity first.

## Directions
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql) and click **Create** in the instance list.
2. On the purchase page, specify the following instance information, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go billing is supported.
 - **Region**: the region where the instance is actually deployed to. To minimize delay, we recommend the same region as the CVM instance to be connected to.
 - **Availability Zone**: IDCs whose electric power facilities and networks are independenst from each other within the same region. To minimize delay, we recommend the same availability zone as the CVM instance to be connected to.
 - **Network**: the network where the instance is deployed to. This cannot be changed once specified. To minimize delay, we recommend the same network as the CVM instance to be connected to.
 - **Database Version**: the features available vary by PostgreSQL kernel version. For more information, please see official instructions on PostgreSQL [v9.3.5](https://www.postgresql.org/docs/9.3/static/index.html), [v9.5.4](https://www.postgresql.org/docs/9.5/static/index.html), [v10.4](https://www.postgresql.org/docs/10/static/index.html), [v11.8](https://www.postgresql.org/docs/11/index.html), and [v12.4](https://www.postgresql.org/docs/12/release-12-4.html).
 - **Instance Specs**: instance performance and base price depend on its specifications.
 - **Disk**: an SSD disk (local disk) is used by default.
 - **Project**: if instances need to be managed by different teams, assign the instances to the projects of different teams accordingly.
 - **Quantity**: the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit of 10 has been set for this parameter. If you want to purchase more instances, please make multiple purchases.
3. After making the payment, go back to the instance list, and you can view the instance just purchased.

