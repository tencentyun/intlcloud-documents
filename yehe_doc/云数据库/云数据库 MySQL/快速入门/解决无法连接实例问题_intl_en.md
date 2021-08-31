You may encounter various errors when connecting to your TencentDB for MySQL instance.
This document describes how to troubleshoot such errors.

<span id = "wfljcjwt"></span>
## Common Problems
### Different network types
If the networks of a CVM instance and a TencentDB for MySQL instance are of different types, the former cannot connect to the latter directly over the private network.

#### The CVM instance uses a VPC, while the TencentDB for MySQL instance uses the classic network
- **Solution 1 (recommended)**: switch the TencentDB for MySQL instance from classic network to VPC as instructed in [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915).
>!
>- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- When the network is switched from classic network to VPC, it cannot be switched back to classic network.
>- The VPC connection takes effect immediately after the switch. The original IP will become invalid after 24 hours by default. If the reclaim time of an old IP is set to 0 hours, the old IP will be reclaimed immediately after the network is changed. Please migrate the instances associated with the current instance to the VPC in time to ensure connectivity of the associated instances.
- **Solution 2**: purchase a new CVM instance that resides in the classic network (the existing CVM instance cannot be migrated from VPC to classic network). However, VPC is more secure than classic network and thus highly recommended.

- **Solution 3**: connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, and we recommend you use VPC.

#### The CVM instance uses the classic network, while the TencentDB for MySQL instance uses a VPC
- **Solution 1 (recommended)**: migrate the CVM instance from classic network to VPC. For detailed directions, please see [Switching to VPC](https://intl.cloud.tencent.com/document/product/213/20278).
>!  
>- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- You need to unbind private/public network CLB instances and ENIs and release auxiliary IPs of the primary ENI before migration and bind them again after migration.
>- The CVM instance will be restarted during migration. Do not perform other operations on it.
>- Check the instance status after migration and verify whether private network connection and remote login work properly.
>- The switch from classic network to VPC is irreversible. After the switch to a VPC, the CVM instance cannot communicate with Tencent Cloud services in the classic network.
- **Solution 2**: use [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807).

- **Solution 3**: connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, and we recommend you use VPC.

<span id = "dybt"></span>
### Different regions
If the regions of a CVM instance and a TencentDB for MySQL instance are different, even when they are in the same VPC, the former cannot connect to the latter directly over the private network.

- **Solution 1**: use a CVM instance in the same account, region, and VPC as the TencentDB for MySQL instance to connect.

- **Solution 2**: connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, and we recommend you use VPC.

<span id = "sywlbt"></span>
### Different VPCs
By default, the CVM and TencentDB for MySQL instances can interconnect over the private network only if they are in the same VPC. If they are in different VPCs, interconnection over the private network can be achieved in the following ways:
- **Solution 1 (recommended)**: migrate the TencentDB for MySQL instance to the VPC of the CVM instance as instructed in [Network Switch](https://intl.cloud.tencent.com/document/product/236/31915).
-  **Solution 2**: create a [peering connection]https://intl.cloud.tencent.com/document/product/553) between the two VPCs.
Otherwise, the instances can only interconnect over the public network, which has poor performance, security, and stability.

<span id = "aqzpzyw"></span>
### Incorrect security group configuration
If the security groups of the CVM instance and the TencentDB for MySQL instance are incorrectly configured, the former cannot connect to the latter directly over the private or public network.

#### The security group of the CVM instance is incorrectly configured
To enable the CVM instance to connect to the TencentDB for MySQL instance, you need to configure an outbound rule in the security group of the CVM instance. **If the destination of the outbound rule isn't 0.0.0.0/0 and the protocol port isn't ALL**, the IP and port of the TencentDB for MySQL instance should be added to the rule.
1. Go to the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM Console and click the name of the CVM-bound security group to enter its details page.
2. On the **Outbound Rules** tab, click **Add Rule**.
Select "MySQL(3306)" as "Type", enter your TencentDB for MySQL IP address (range) in "Target", and select "Allow" for "Policy".

#### The security group of the TencentDB for MySQL instance is incorrectly configured
To enable the CVM instance to connect to the TencentDB for MySQL instance, you need to configure an inbound rule in the security group of the TencentDB for MySQL instance. **If the source of the inbound rule isn't 0.0.0.0/0 and the protocol port isn't ALL**, the IP and port of the CVM instance should be added to the rule. 
1. Go to the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM Console and click the name of the TencentDB for MySQL-bound security group to enter its details page.
2. On the **Inbound Rules** tab, click **Add Rule**.
Enter the allowed IP address (or range) and port to be opened (private network port of the TencentDB for MySQL instance) and select "Allow".
Select "MySQL(3306)" as "Type", enter your CVM IP address (range) in "Source", and select "Allow" for "Policy".
>!  
>- TencentDB for MySQL uses private network port 3306 by default and supports customizing the port. If the default port is changed, the new port should be opened in the security group.
>- Port 3306 of the instance should be opened in the inbound rule of the security group.

<span id = "sjkzhzjpzyw"></span>  
### The host configuration of the database account is incorrect
If a host address is specified for the database account, the TencentDB for MySQL instance cannot be connected to from other addresses.

By modifying the host address authorized by the database account in the TencentDB for MySQL Console, you can control connection to the database so as to improve connection security.

1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance name or **Manage** in the "Operation" column to enter the instance management page.
3. Select **Database Management** > **Manage Account**, find the account for which to modify the host, and select **More** > **Modify Host** in the "Operation" column.
4. In the pop-up dialog box for modifying host, enter the new host address and click **OK**.
>?The host address can be an IP and contain `%` (indicating not to limit the IP range). Multiple hosts should be separated by line breaks, spaces, semicolons, commas, or vertical bars.
> - Example 1: enter `%` to indicate not to limit the IP range, that is, clients at all IP addresses are allowed to use this account to connect to the database.
> - Example 2: enter `10.5.10.%`, which means that clients whose IP range is within `10.5.10.%` are allowed to use this account to connect to the database.


<span id = "wllxvpdff"></span>
## How to Check Network Type/VPC
To enable connection between CVM and TencentDB for MySQL instances over the private network, they must be under the same account and in the same VPC in the same region, or both in the classic network.
>?
> CVM and TencentDB for MySQL instances must be under the same account:
>- If the "Network" fields in the instance lists both show "Classic Network" or "VPC", it means that the networks of the CVM and TencentDB for MySQL instances are of the same type.
>- If the "Network" fields in the instance lists both show the same "VPC" (in the same region), it means that the CVM and TencentDB for MySQL instances are in the same VPC.
>
- **View CVM network type/VPC**: log in to the [CVM Console](https://console.cloud.tencent.com/cvm/instance) and view "Network" in the instance list.
![](https://main.qcloudimg.com/raw/4a113e0488aab66d612f989ce04dbfdf.png)
- **View TencentDB for MySQL network type/VPC**: log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb) and view "Network" in the instance list.
![](https://main.qcloudimg.com/raw/3ae00005e16d22f1e73fb85b607a1274.png)

