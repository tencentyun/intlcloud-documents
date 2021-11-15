TencentDB now supports the IPv6 feature. You can access databases over a private or public IPv6 address.

## Notes
- TencentDB that supports IPv6: MySQL, MongoDB, MariaDB, TDSQL, PostgreSQL, Redis, CTSDB, and TcaplusDB.
- Region that supports IPv6: Beijing Zone 5, Guangzhou Zone 4, Shanghai Zone 4, Chengdu Zone 1, and Nanjing Zone 1.
- You need select an [IPv6 VPC](https://intl.cloud.tencent.com/document/product/215/32382) when purchasing an instance.
- TencentDB for MongoDB, Redis, CTSDB, and TcaplusDB do not support public network access. They only support access over a private IPv6 (or IPv4) address.

## Directions
### Step 1. Enable access over IPv6
1. Log in to the [TencentDB purchase page](https://buy.cloud.tencent.com/cdb?regionId=8) and select the desired TencentDB on the navigation bar at the top.
>?You can purchase a TcaplusDB instance on the cluster list page in the [console](https://console.cloud.tencent.com/tcaplusdb/app).
2. Select "IPv6 address access is supported" in the "IP Version" section on the purchase page.
![](https://main.qcloudimg.com/raw/9e5b86c845d03759ea33e73858913e3d.png)
>?After an instance is purchased, access over IPv6 will be automatically enabled and a private IPv6 address will be automatically assigned.

### Step 2. Enable a public IPv6 address (optional)
1. Log in to the [TencentDB Console](https://console.cloud.tencent.com/cdb) and select the desired TencentDB on the left sidebar.
2. Click an instance name in the instance list to enter the details page. In the "Public IPv6 Address" section, click **Enable** to enable and assign a public IPv6 address.
![](https://main.qcloudimg.com/raw/fde252d7b2523584cb364e1361a3567d.png)

### Step 3. Use an IPv6 address to access a database
#### Accessing a database over a private network address
A CVM instance can be used to access the private IPv6 address of a TencentDB instance. This method relies on the high-speed private network of Tencent Cloud and features low delay.
  - The CVM and TencentDB instances must be under the same account and in the same VPC in the same region.
  - The private IPv6 address can be viewed in the instance/cluster list or on the instance/cluster details page in the [console](https://console.cloud.tencent.com/cdb).

#### Accessing a database over a public network address
You can use a public IPv6 address to access a TencentDB instance that has enabled public network access.
  - The public IPv6 address can be viewed on the instance/cluster details page in the [console](https://console.cloud.tencent.com/cdb).
  - Public network access to TencentDB is suitable for development or auxiliary database management but not for actual business access, because uncontrollable factors may cause public network access to be unavailable, such as DDoS attacks and sudden surges in access traffic.
