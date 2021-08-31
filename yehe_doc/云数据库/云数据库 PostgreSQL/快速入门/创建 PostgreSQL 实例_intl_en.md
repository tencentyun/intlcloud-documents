This document describes how to create a TencentDB for PostgreSQL instance in the console.

## Prerequisites
You have registered a [Tencent Cloud account](https://intl.cloud.tencent.com/register) and completed [identity verification](https://console.cloud.tencent.com/developer).

## Directions
1. Log in to the [TencentDB for PostgreSQL purchase page](https://Intl.buy.cloud.tencent.com/pgsql), specify the database instance information as needed, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: pay-as-you-go.
 - **Region**: the region where the instance is actually deployed. To minimize delay, we recommend the same region as the CVM instance to be connected to.
 - **Availability Zone**: physical IDCs whose electric power facilities and networks are independent from each other within the same region. To minimize delay, we recommend the same availability zone as the CVM instance to be connected to.
 - **Network**: the network where the instance is deployed. This cannot be changed once specified. To minimize delay, we recommend the same network as the CVM instance to be connected to.
 - **Database Version**: the features available vary by PostgreSQL kernel version. For more information, please see official instructions on PostgreSQL [v10.4](https://www.postgresql.org/docs/10/static/index.html), [v11.8](https://www.postgresql.org/docs/11/index.html), and [v12.4](https://www.postgresql.org/docs/12/release-12-4.html).
 - **Instance Specs**: instance performance and base prices depend on its specification.
 - **Disk**: SSD disk (local disk) is used by default.
 - **Username**: the account name can contain 1–16 letters (case-insensitive), digits, or underscores (_). It cannot be `postgres` or start with a digit or `pg\_`.
 - **Password**: the password can contain 8–32 characters. We recommend you use a password of at least 12 characters. It cannot start with a slash (/) and must contain all the following types of characters:
     - Lowercase letters (a–z)
     - Uppercase letters (A–Z)
     - Digits (0–9)
     - Special symbols `()~!@#$%^&*-+=_|{}[]:;'<>,.?/`
 - **Project**: if instances need to be managed by different teams, assign the instances to the projects of different teams accordingly.
 - **Quantity**: the number of instances that can be purchased at a time. To avoid faulty operations, an upper limit of 10 has been set for this parameter. If you want to purchase more instances, please make multiple purchases.
2. After the purchase is completed, you will be redirected to the [instance list](https://console.cloud.tencent.com/postgres). After the status of the instance changes to **Running**, the instance can be connected to.

## Subsequent Operations
You can use a standard SQL client to connect to the TencentDB for PostgreSQL instance at its private or public address. For more information, please see [Connecting to TencentDB for PostgreSQL Instance](https://intl.cloud.tencent.com/document/product/409/34626).
