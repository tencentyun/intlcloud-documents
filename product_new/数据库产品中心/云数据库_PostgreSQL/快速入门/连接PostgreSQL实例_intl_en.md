## Operation Scenarios
After initializing a TencentDB for PostgreSQL instance, you can use a standard SQL client to access it over the private network or public network.
- **Private network access**: a CVM instance can be used to access the private network address automatically assigned to the TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. Both instances should be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) or in the basic network.
>For more information on connection between CVM and database instances in different VPCs (under the same account/different accounts; in the same region/different regions) over the private network, please see [Peering Connection](https://cloud.tencent.com/document/product/553/18827).
- **Public network access**: TencentDB for PostgreSQL can be accessed by using a public network address.
>
>- For public network access, the database instance's public IP needs to be enabled, which may expose the database service to attacks or intrusions on the public network. Therefore, it is recommended to log in to the database over the private network.
>- Public network access to TencentDB is suitable for development or auxiliary management of databases but not for formal business access, as potentially uncontrollable factors may lead to unavailability of the public network access, such as DDoS attacks and bursts of high-traffic access.
>- Instances that currently support public network access are available only in Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), and Silicon Valley.

The following describes how to access TencentDB for PostgreSQL on Windows over the private network and public network.
## Directions
1. Download and install a standard SQL client as instructed in [Getting Started with Windows CVM](https://intl.cloud.tencent.com/document/product/213/2764) or locally.
>pgAdmin is used in this example. You can download the appropriate installer based on your system version [here](https://www.pgadmin.org/download/).
>
2. In pgAdmin, select **Object** > **Create** > **Server**.
![](https://main.qcloudimg.com/raw/38db0fb15e9de97762362a7afb105796.png)
3. In the **Create - Server** dialog box, enter the information such as name, host IP address, port number, username, and password and then click **Save**.
 - Host IP address and port number: you can go to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and view them in **Private Network Address** or **Public Network Address** on the instance details page. If public network access is not enabled, please see [Enabling Public Network Access](#kqww).
>Here, the private network address is VIP; database instances are accessed by connecting to the gateway cluster rather than the physical servers of database instances directly. Therefore, the private IP will remain unchanged in the event of server failures or master/slave switchover.
 - Username and password: use the database admin username and password set when the instance is initialized. If you forget the password, you can go to the account management page in the console to reset it.
![](https://main.qcloudimg.com/raw/ef6b1975a212ee352adda4dd4e1159e7.png)
4. Then, select **Databases** > **postgres** on the left sidebar to view the connected server (database instance).
![](https://main.qcloudimg.com/raw/ede1361fb76d38deaf9cf22d3a43e8f3.png)

<span id = "kqww"></span>
#### Enabling public network access
1. Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql). In the instance list, click the instance name or **Manage** in the "Operation" column to enter the instance details page.
2. Find **Public Network Address** in the basic info section on the instance details page and click **Enable**.
3. Click **OK** in the pop-up window and the request to enable public network access will be processed.
4. Once enabled successfully, the public network address can be found in the basic info section.
