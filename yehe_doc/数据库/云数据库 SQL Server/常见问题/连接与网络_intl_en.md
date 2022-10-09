### How do I create an instance and connect to a database?
You can manage databases in the TencentDB for SQL Server console. For detailed directions, see [Creating TencentDB for SQL Server Instance](https://intl.cloud.tencent.com/document/product/238/31571).

### How do I connect to TencentDB for SQL Server?
1. To connect to TencentDB for SQL Server from a Windows CVM instance, we recommend you connect over the private network, which has a higher transfer speed and security. The following three prerequisites must be met before you can do so:
 - The CVM and TencentDB for SQL Server instances are under the same Tencent Cloud root account.
 - The CVM and TencentDB for SQL Server instances are in the same region.
 - The CVM and TencentDB for SQL Server instances are in the same VPC or classic network.
For more information, see [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626).
If the CVM and TencentDB for SQL Server instances are under different Tencent Cloud root accounts, in different regions under the same root account, or in different VPCs in the same region under the same root account, we recommend you use [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) for interconnection.
2. To connect to a TencentDB for SQL Server instance from a local system, we recommend you use VPN Connections, Direct Connect, or CCN as described in [Overview](https://intl.cloud.tencent.com/document/product/1037/32679), [Getting Started](https://intl.cloud.tencent.com/document/product/216/7557), or [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) respectively for interconnection, which are secure and guarantee a low network latency. To reduce costs, you can also use the public network for interconnection by [directly enabling the public network address](https://www.tencentcloud.com/document/product/238/50230) in the console or by [enabling public network access through CLB](https://www.tencentcloud.com/document/product/238/48066). For more information, see [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

If your TencentDB for SQL Server instance is on the Dual-Server High Availability/Cluster Edition, you can use CLB to enable public network access.

[](id:FWYSJK)
### How do I access a TencentDB for SQL Server instance from a CVM instance over the private network?
To connect to a TencentDB for SQL Server instance from a CVM instance over the private network, the following three prerequisites must be met:
- The CVM and TencentDB for SQL Server instances are under the same Tencent Cloud root account.
- The CVM and TencentDB for SQL Server instances are in the same region.
- The CVM and TencentDB for SQL Server instances are in the same VPC or classic network.

For more information, see [Connecting to TencentDB for SQL Server Instance from Windows CVM Instance](https://intl.cloud.tencent.com/document/product/238/11626).

### What should I check when interconnecting a CVM instance and a TencentDB for SQL Server instance over the private network?
To connect to a TencentDB for SQL Server instance from a CVM instance over the private network, the following three prerequisites must be met:
- The CVM and TencentDB for SQL Server instances are under the same Tencent Cloud root account.
- The CVM and TencentDB for SQL Server instances are in the same region.
- The CVM and TencentDB for SQL Server instances are in the same VPC or classic network.

### How do I view the private network address of a TencentDB for SQL Server instance?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and view it in the instance list. You can also click an instance ID to enter the **Instance Details** page and view it.

### How do I access a TencentDB for SQL Server instance from a CVM instance under another Tencent Cloud root account?
CVM and TencentDB for SQL Server instances under different Tencent Cloud accounts cannot interconnect over the private network. We recommend you migrate the TencentDB for SQL Server instance to the account of the CVM instance.
If you need to keep the instances under different Tencent Cloud accounts, make sure that their are both in VPCs and create a CCN instance as described in [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) between the two VPCs for interconnection.

[](id:BTDYNWHT)
### How do I interconnect a CVM instance and a TencentDB for SQL Server instance in different regions under the same Tencent Cloud root account over the private network?
CVM and TencentDB for SQL Server instances in the same AZ or different AZs in the same region can interconnect over the private network, while instances in different regions cannot.
If you need to keep the instances in different regions, make sure that their are both in VPCs and create a CCN instance as described in [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) between the two VPCs for interconnection.

### How do I interconnect a CVM instance and a TencentDB for SQL Server instance in different VPCs in the same region under the same Tencent Cloud root account over the private network?
CVM and TencentDB for SQL Server instances in different VPCs cannot interconnect over the private network. We recommend you migrate the TencentDB for SQL Server instance to the VPC of the CVM instance.
If you need to keep the instances in different VPCs, create a CCN instance as described in [Getting Started with the CCN](https://intl.cloud.tencent.com/document/product/1003/31985) between the two VPCs for interconnection.

### How do I interconnect a CVM instance and a TencentDB for SQL Server instance in different types of networks in the same region under the same Tencent Cloud root account over the private network?
CVM and TencentDB for SQL Server instances in different types of networks cannot interconnect over the private network. We recommend you change the classic network of the CVM or TencentDB for SQL Server instance to VPC and ensure that the instances are in the same VPC for interconnection over the private network.

### How do I interconnect a CVM instance and a TencentDB for SQL Server instance in different AZs in the same region under the same Tencent Cloud root account over the private network?
CVM and TencentDB for SQL Server instances in different AZs in the same region may or may not be in the same VPC.
- If they are in different AZs in the same VPC, they can interconnect over private network.
- If they are in different VPCs, they cannot interconnect over the private network. You need to change their VPCs to the same VPC. For more information, see [Changing Network (from VPC to VPC)](https://intl.cloud.tencent.com/document/product/238/46497).

### Can I interconnect a CVM instance and a TencentDB for SQL Server instance in different AZs in the same VPC under the same Tencent Cloud root account?
Yes. Instances in different AZs but in the same VPC interconnect over private network by default.

[](id:BDFWQFWSJK)
### How do I access a TencentDB for SQL Server instance from a local server?
To connect to a TencentDB for SQL Server instance from a local server, we recommend you use [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Direct Connect](https://intl.cloud.tencent.com/document/product/216), or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) for interconnection, which are more secure and guarantee a low network latency.
To reduce costs, you can use the public network for interconnection by [directly enabling the public network address](https://www.tencentcloud.com/document/product/238/50230) in the console or by [enabling public network access through CLB](https://www.tencentcloud.com/document/product/238/48066). For more information, see [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

If your TencentDB for SQL Server instance is on the Dual-Server High Availability/Cluster Edition, you can use CLB to enable public network access.

### How do I connect to a TencentDB for SQL Server instance without a CVM instance?
If you don't have a CVM instance, we recommend you use [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Direct Connect](https://intl.cloud.tencent.com/document/product/216), or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) to interconnect the networks and then connect to the TencentDB for SQL Server instance. For more information, see [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

### How do I switch a TencentDB for SQL Server instance from VPC A to VPC B?
You can change the VPC of a TencentDB for SQL Server instance as instructed in [Changing Network (from VPC to VPC)](https://intl.cloud.tencent.com/document/product/238/46497).

### How do I switch between the classic network and VPC for a TencentDB for SQL Server instance?
You can only switch from classic network to VPC for a TencentDB for SQL Server instance but not vice versa. For more information, see [Switching from Classic Network to VPC](https://intl.cloud.tencent.com/document/product/238/46498). Classic network will be deactivated in December 2022.

### How do I migrate a TencentDB for SQL Server instance from classic network to VPC?
You can switch from classic network to VPC for a TencentDB for SQL Server instance. For more information, see [Switching from Classic Network to VPC](https://intl.cloud.tencent.com/document/product/238/46498).

### How do I enable public network access for a TencentDB for SQL Server instance?
If your TencentDB for SQL Server instance is on the High Availability Edition or Cluster Edition, you can directly enable the public network address in the console or enable public network access through CLB. For more information, see [Enabling/Disabling Public Network Address](https://www.tencentcloud.com/document/product/238/50230) or [Enabling Public Network Access Through CLB](https://www.tencentcloud.com/document/product/238/48066).

### How do I use the port mapping feature of SSH2 to connect to and manage a TencentDB for SQL Server instance from the internet?
For security considerations, if your business doesn't allow enabling the public network address, you can use the port mapping feature of SSH2 to connect to, configure, and manage an instance from the internet. For detailed directions, see [Connecting to TencentDB for SQL Server Instance from Local System](https://intl.cloud.tencent.com/document/product/238/11627).

[](id:ZDCLSJK)
### Does my application need to support automatic reconnection to TencentDB for SQL Server?
We recommend you configure automatic reconnection for your application for a higher availability. After a database is switched or migrated, the application can recover automatically with no manual intervention needed. We also recommend you use a persistent connection to connect your application to the database, as non-persistent connections consume many resources and compromise the performance.

### Can I access a TencentDB for SQL Server replica instance?
TencentDB for SQL Server supports the mode of primary + replica + read-only instances. Only the primary and read-only instances can be accessed, while the replica instance is used for backup only and doesn't support business access.

### Will a primary/replica switch affect the connection address?
A primary/replica switch won't change the connection address, but the IP address on the backend will change, and there will be a momentary disconnection during the switch.

### How do I configure a security group in TencentDB for SQL Server?
A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group.
TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For more information, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).

### Can I use a security group in TencentDB for SQL Server to control the classic network?
TencentDB for SQL Server security groups currently only support network access control for VPCs and public network but not the classic network.

### Can I select the SQL Server (1433) port as the type when adding an inbound rule to a security group?
When adding a security group, you can select **SQL Server (1433)** for **Type** to open protocol port 1433. For more information, see [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789).

[](id:SZSLWHQJ)
### How do I set the instance maintenance time in TencentDB for SQL Server?
Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver), click the ID of the target instance in the instance list to enter the instance details page, and click **Modify** in **Maintenance Info**. For more information, see [Setting Instance Maintenance Information](https://intl.cloud.tencent.com/document/product/238/35785).

### Will TencentDB for SQL Server be disconnected during the maintenance?
If data migration needs to be performed during the maintenance of TencentDB for SQL Server, instance switch is accompanied by a disconnection from the database lasting for just seconds. Make sure that your business has a reconnection mechanism. For more information, see [Setting Instance Maintenance Information](https://intl.cloud.tencent.com/document/product/238/35785).

### Why can't I connect to TencentDB for SQL Server?
Troubleshoot as follows if you can't connect to TencentDB for SQL Server:
- Check whether the CVM instance can properly connect to the port of the address of the TencentDB for SQL Server instance by running `telnet <connection address> <port number>`. If the port can be accessed, the network is normal; otherwise, check whether the CVM and TencentDB for SQL Server instances are in the same VPC and same security group. If you use the private network for connection, the instances must be in the same VPC, and the connection can be initiated from CVM only.
- Check whether the connection IP and port are correct and separated by comma.
- Check whether the status of the TencentDB for SQL Server instance is abnormal.
- Check whether the database username and password are correct and try resetting the password.
- Try restarting the TencentDB for SQL Server instance and check whether the problem is resolved.

### What should I do If I fail to connect to TencentDB for SQL Server?
1. If the connection to a TencentDB for SQL Server instance from a Windows CVM instance failed:
 - Troubleshoot network problems.
    - Check whether the CVM and TencentDB for SQL Server instances are in the same VPC in the same region.
    - Check security group rules. When a database in the security group is accessed from an address not in the security group, you need to add a corresponding inbound rule to the security group as instructed in [Configuring Security Group](https://intl.cloud.tencent.com/document/product/238/35789). Check CVM security groups, internal firewalls, and internal/custom security policies, and open port 1433 for the specified TencentDB instance IP.
    - Check whether the CVM instance can properly connect to the port of the address of the TencentDB for SQL Server instance by running `telnet <connection address> <port number>`. If the port can be accessed, the network is normal.
 - Troubleshoot instance problems.
    - If the network is normal, check the instance monitoring information in the console. If the instance load is too high or there is no or intermittent monitoring data, the instance is abnormal.

2. If the connection to a TencentDB for SQL Server instance from a local IDC fails:
 - Troubleshoot network problems.
    - To connect to a TencentDB instance from a local server, you first need to interconnect the local and cloud networks. We recommend you use [VPN Connections](https://intl.cloud.tencent.com/document/product/1037), [Direct Connect](https://intl.cloud.tencent.com/document/product/216), or [CCN](https://intl.cloud.tencent.com/document/product/1003/31985) for interconnection, which are more secure and guarantee a low network latency.
    - Check whether the server can properly connect to the port of the address of the TencentDB for SQL Server instance by running `telnet <connection address> <port number>`. If the port can be accessed, the network is normal.
    - If telnet fails, the network is disconnected, and you need to check local security group policies and VPC routing configurations, open port 1433 for the specified database IP, and perform online and offline CVM instance connectivity tests.
  - Troubleshoot instance problems.
    - If the network is normal, check the instance monitoring information in the console. If the instance load is too high or there is no or intermittent monitoring data, the instance is abnormal. 
