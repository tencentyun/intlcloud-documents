
TencentDB for SQL Server supports two types of networks: **VPC and basic network**.

## Network Limitations
- Tencent Cloud services in the same region can communicate with one another over the private network.
- A CVM instance in a VPC can communicate with a TencentDB for SQL Server instance on the basic network in a different AZ in the same region only after a subnet is configured and a VPC IP is assigned.
- Tencent Cloud services on the basic network in different regions cannot communicate with one another over the private network. They can communicate across VPCs only after a **peering connection** is configured.
Currently, TencentDB for SQL Server currently doesn't support public IP. If you need to use a public IP, you can use the port mapping function of SSH2 to connect to, configure, and manage an instance from the internet. For more information, see [Connect to Instance](http://intl.cloud.tencent.com/document/product/238/11627).
> When purchasing TencentDB for SQL Server, it is recommended to select the same region as your CVM instance to reduce access delay.

## Network Connectivity Test
The network connectivity test tool provided on the [TencentDB for SQL Server purchase page](https://buy.cloud.tencent.com/sqlserver#/) can be used to check whether there are CVM instances in the selected region/AZ and network type that can communicate with TencentDB for SQL Server over the private network.
![](https://main.qcloudimg.com/raw/2621c32856e4449fb646747b5c586806.png)
Click **View Details** to view the information of eligible CVM instances, including ID/instance name, AZ, configuration (CPU, memory, disk, and network), and master IP address. You can also use the search function to quickly determine whether a specific CVM instance can communicate with TencentDB for SQL Server over the private network.
![](https://main.qcloudimg.com/raw/1f50bbd8908a652c5d87eef2fdc489be.png)