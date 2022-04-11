This document describes how to create a TencentDB for PostgreSQL instance in the console.

## Prerequisites
You have [registered a Tencent Cloud account](https://Intl.cloud.tencent.com/register) and [completed identity verification](https://console.cloud.tencent.com/developer).

## Directions
1. Log in to the [TencentDB for PostgreSQL purchase page](https://buy.intl.cloud.tencent.com/pgsql), specify the database instance information as needed, confirm that everything is correct, and click **Buy Now**.
 - **Billing Mode**: Pay-as-you-go billing is supported.
 - **Region**: The region where the instance is actually deployed. To minimize delay, we recommend the same region as the CVM instance to be connected to.
 - **AZ**: Physical IDCs where electric power facilities and networks are independent from each other within the same region. To minimize delay, we recommend the same AZ as the CVM instance to be connected to. Both multi-AZ deployment (the primary and standby nodes are in different AZs) and single-AZ deployment (the primary and standby nodes are in the same AZ) are supported. Specific primary and standby AZs are as displayed on the actual purchase page.
 - **Network**: The network where the instance is deployed. To minimize delay, we recommend the same network as the CVM instance to be connected to.
>?VPC: It is a logically isolated network space in Tencent Cloud. In a VPC, you can customize IP ranges, IP addresses, and routing policies.
>
 - **Architecture**: TencentDB for PostgreSQL supports the dual-server high-availability (one-primary-one-standby) architecture by default.
 - **Database Version**: The features available vary by PostgreSQL kernel version. For more information, see the official descriptions of PostgreSQL [10](https://www.postgresql.org/docs/10/static/index.html), [11](https://www.postgresql.org/docs/11/index.html), [12](https://www.postgresql.org/docs/12/release-12-4.html), and [13](https://www.postgresql.org/docs/13/index.html).
 - **Instance Specification**: Instance performance and base prices depend on its specification.
 - **Disk**: An SSD disk (local disk) is used by default.
 - **Backup Space**: You will receive 50% of the instance capacity for free to use as backup capacity. Any usage exceeding this complimentary capacity is currently free as well.
 - **Instance Name**: Name the instance now or later with up to 60 letters, digits, underscores, and hyphens.
 - **Character Set**: TencentDB for PostgreSQL supports UTF8 and LATIN1 character sets.
 - **Username**: The account name can contain 1–16 letters (case-insensitive), digits, or underscores. It cannot be `postgres` or start with a digit or `pg\_`.
 - **Password**: The password can contain 8–32 characters. We recommend you use a password of at least 12 characters. It cannot start with a slash (/) and must contain all the following types of characters:
     - Lowercase letters (a–z)
     - Uppercase letters (A–Z)
     - Digits (0–9)
     - Special symbols `()~!@#$%^&*-+=_|{}[]:;'<>,.?/`
 - **Project**: If instances need to be managed by different teams, assign the instances to the projects of different teams accordingly.
 - **Security Group**: It serves as a stateful virtual firewall with filtering feature for configuring network access control for one or more TencentDB instances. It is an important network security isolation tool provided by Tencent Cloud.
 - **Tag**: It facilitates resource categorization and management.
 - **Quantity**: The number of instances that can be purchased at a time. To avoid faulty operations, an upper limit of 10 has been set for this parameter. If you want to purchase more instances, make multiple purchases.
 - **Terms of Service**: Read and click it. For more information, see [Terms of Service](https://intl.cloud.tencent.com/document/product/409/35547).
2. After the purchase is completed, you will be redirected to the [instance list](https://console.cloud.tencent.com/postgres). After the status of the instance changes to **Running**, the instance can be connected to.

## Subsequent Operations
You can use a standard SQL client to connect to the TencentDB for PostgreSQL instance at its private or public network address. For more information, see [Connecting to TencentDB for PostgreSQL Instance](https://intl.cloud.tencent.com/document/product/409/34626).
