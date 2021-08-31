You can use a standard SQL client to access it over the private network or public network.
- **Private network access**: a CVM instance can be used to access the private network address automatically assigned to the TencentDB instance. This access method relies on the high-speed private network of Tencent Cloud and features low delay. The two instances must be under the same account and in the same [VPC](https://intl.cloud.tencent.com/document/product/215/535) in the same region or both must be in the classic network.
>?CVM and TencentDB instances in different VPCs (under the same or different accounts in the same or different regions) can be interconnected over private network through [Peering Connection](https://intl.cloud.tencent.com/document/product/553/18827).
- **Public network access**: TencentDB for PostgreSQL can be accessed by using a public network address.
>!
>- For public network access, the database instance's public IP needs to be enabled, which may expose your database service to attacks or intrusions on the public network. Therefore, it is recommended to log in to the database over the private network.
>- Public network access to TencentDB is suitable for development or auxiliary management of databases but not for business access in the production environment, as potentially uncontrollable factors may lead to unavailability of the public network access, such as DDoS attacks and bursts of high-traffic access.
>- Instances that currently support public network access are available only in Guangzhou, Shanghai, Beijing, Chengdu, Hong Kong (China), and Silicon Valley.

The following describes how to connect to a TencentDB for PostgreSQL instance from Windows and Linux CVM instances over the private and public networks.

### Connecting from a Windows CVM Instance
1. Download and install a standard SQL client in a Windows CVM instance or locally. For more information about how to log in to a CVM instance, please see [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).
>?Take pgAdmin for example. You can download an installer [here](https://www.pgadmin.org/download/) based on your operating system version.
2. In pgAdmin, select **Object** > **Create** > **Server**.
![](https://main.qcloudimg.com/raw/38db0fb15e9de97762362a7afb105796.png)
3. In the **Create - Server** dialog box, enter the information such as host name/address, port number, username, and password and then click **Save**.
 - Host name/address and port number: you can go to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql) and view them in **Private IPv4/IPv6 Address** or **Public IPv4/IPv6 Address** in the **Basic Info** section on the instance details page. If the public IP is not enabled, please see [Enabling Public Network Access](#kqww).
>?Here, the private IP is VIP; database instances are accessed by connecting to the gateway cluster rather than the physical servers of database instances directly. Therefore, the private IP will remain unchanged in the event of server failures or primary/standby switchover.
 - Username and password: use the database admin username and password set when the instance is initialized. If you forget the password, you can go to the account management page in the [console](https://console.cloud.tencent.com/pgsql) to reset it.
![](https://main.qcloudimg.com/raw/ef6b1975a212ee352adda4dd4e1159e7.png)
4. Then, select **Databases** > **postgres** on the left sidebar to view the connected server (database instance).
![](https://main.qcloudimg.com/raw/ede1361fb76d38deaf9cf22d3a43e8f3.png)

### Connecting from a Linux CVM Instance
1. Install a psql client via yum in a Linux CVM instance or locally. For more information about how to log in to a CVM instance, please see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517).
2. To install a psql client, please follow the instructions in [Restoring PostgreSQL Data on CVMs > Install PostgreSQL](https://intl.cloud.tencent.com/document/product/409/11642) to install PostgreSQL, as the psql client will be installed along with PostgreSQL.
3. Run the following command to log in to the PostgreSQL database:
```
psql -U username -h access address -p port -d postgres
```
>?To access from a CVM instance in the same VPC of the database instance, use the private IP of the database instance as the **access address**. To access from a Linux server on the internet, use the public IP of the database instance as the **access address**.

### [Appendix. Enabling Public Network Access]
1. Log in to the [TencentDB for PostgreSQL console](https://console.cloud.tencent.com/pgsql). In the instance list, click the instance ID/name or **Manage** in the **Operation** column to access the instance details page.
2. Click **Enable** next to **Public IPv4/IPv6 Address** in the **Basic Info** section on the instance details page.
![](https://main.qcloudimg.com/raw/2370f85dcc86010f5cfbdee1fa333745.png)
3. Click **OK** in the pop-up window and the request to enable public IP will be processed.
4. Once enabled successfully, the public IP can be found in the **Basic Info** section.
