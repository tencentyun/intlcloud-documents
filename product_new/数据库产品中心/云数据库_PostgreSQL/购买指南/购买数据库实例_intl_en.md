## Operation Scenarios
This document describes how to create a database instance in the TencentDB for PostgreSQL Console.

## Prerequisites
You have already [signed up for a Tencent Cloud account](https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F).

## Directions
1. Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and click **Create** in the instance list.
2. Specify the information of the database instance as needed.
 - **Billing Mode**: pay-as-you-go billing based on actual usage is supported.
 - **Region**: this is the region where the instance is actually deployed. You are recommended to choose the same region as the CVM instance to connect to in order to minimize delay.
 - **AZ**: this is a physical IDC that has independent power supply and network. You are recommended to choose the same AZ as the CVM instance to connect to in order to minimize delay.
 - **Network Type**: this is the network in which the instance resides. This cannot be changed once specified. You are recommended to choose the same network as the CVM instance to connect to in order to minimize delay.
 - **Database Kernel Version**: the features available vary by PostgreSQL database kernel version. For more information, please see [9.3.5](https://www.postgresql.org/docs/9.3/static/index.html), [9.5.4](https://www.postgresql.org/docs/9.5/static/index.html), and [10.4](https://www.postgresql.org/docs/10/static/index.html).
 - **Instance Specification**: instance performance and base price depend on its specification.
 - **Disk**: an SSD disk (local disk) is used by default.
 - **Project**: if you want different databases to be managed by different teams, you can specify the projects under different teams for the databases.
 - **Maximum Purchase Quantity**: this is the number of instances that can be purchased at a time. To prevent faulty operations, an upper limit of 10 has been set. If you need more instances, you can purchase multiple times.
3. After confirming that everything is correct, click **Buy Now**.
4. After purchase, you will be redirected to the payment page. After making the payment, you can view the instance just purchased in the instance list.

