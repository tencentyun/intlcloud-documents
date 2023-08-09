## Issue Description
- [Symptom 1](id:xz1): Failed to connect to or log in to a TencentDB for MySQL instance from a CVM instance.
- [Symptom 2](id:xz2): Failed to connect to or log in to a TencentDB for MySQL instance from a local device.
- [Symptom 3](id:xz3): Failed to connect to or log in to a TencentDB for MySQL instance from DMC.
![](https://qcloudimg.tencent-cloud.cn/raw/6fd9149e439cab91ff45bb8f9192ec66.png)

## Common Causes
<table>
<thead><tr><th width=15%>Possible Cause</th><th width=35%>Description</th><th width=15%>Possible Cause</th><th width=35%>Description</th></tr></thead>
<tbody><tr>
<td><a href="#cvmj">Network issue 1</a></td><td>The CVM instance is in a VPC but the MySQL instance in the classic network.</td>
<td><a href="#sjkzhzjpzyw">Database account authorization issue</a></td><td>The needed host addresses are not authorized by the database account.</td></tr>
<tr>
<td><a href="#cjmv">Network issue 2</a></td><td>The CVM instance is in the classic network but the MySQL instance in a VPC.</td>
<td><a href="#ljyfwt">Connection command syntax issue</a></td><td>The connection command is incorrect.</td></tr>
<tr>
<td><a href="#cmvbt">Network issue 3</a></td><td>The CVM and MySQL instances are in the same region but different VPCs.</td>
<td><a href="#idyw">IP and port issue</a></td><td>The IP and port in commands or configuration files are incorrect.</td></tr>
<tr>
<td><a href="#dywt">Network issue 4</a></td><td>The CVM and MySQL instances are in different regions and different VPCs.</td>
<td>MySQL instance status</td><td>The MySQL instance is isolated. Go to the <a href="https://console.cloud.tencent.com/mysql/recycle">recycle bin</a> to restore it.</td></tr>
<tr>
<td><a href="#caqzpzyw">Security group issue</a></td><td>The security group configuration of the CVM instance is incorrect.</td>
<td>CVM instance status</td><td>The CVM instance is isolated or shut down. Go to the <a href="https://console.cloud.tencent.com/cvm/instance">console</a> to restore or start it up.</td></tr>
<tr>
<td><a href="#maqzpzyw">Security group issue</a></td><td>The security group configuration of the MySQL instance is incorrect.</td>
<td>Public network access status</td><td>The public network access is disabled for the MySQL instance. To enable it, see <a href="https://www.tencentcloud.com/document/product/236/37788">Connecting to MySQL Instance</a></td></tr>.
</tbody></table>

## Solutions
### Solutions to [symptoms 1 and 2](#xz1)
1. **Use the diagnosis tool to locate the causes**.
You can use the [one-click connectivity checker](#step1) provided in the TencentDB for MySQL console to locate the causes, solve the issues by following the handling suggestions, and connect again.
2. **Locate the causes by yourself**.
If the causes cannot be located by the one-click connectivity checker, you can [locate them by yourself by referring to the following document](#step2).

### Solution to [symptom 3](#xz3)
1. Confirm that the database account has authorized all IPs of DMC servers in the region. For more information on authorization, see [Modifying Host Addresses with Access Permissions](https://intl.cloud.tencent.com/document/product/236/31903). You can also set **%** as the host address authorized by the database account to allow all IPs and only use security groups to control database access.
2. If you confirm that all needed IPs are authorized, then the cause may be incorrect password. Accordingly, you can enter the password again, reset the password, or create a temporary account with sufficient permissions. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901) and [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900).

## Troubleshooting
### Symptoms 1 and 2: Troubleshooting the CVM or local connection issues
#### [Step 1. Use the one-click connectivity checker to locate causes and solve the issues](id:step1)
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the ID of the instance to be checked and access the instance management page.
2. On the instance management page, select the **Connection Check** > **Private Network Check** or **Public Network Check** tab.
>?You can view the private and public network addresses in the **Basic Info** section on the **Instance Details** page.
3. Add CVMs or public network servers that need to access the MySQL instance.
 - Private network check: Click **Add CVMs to Access This Instance**.
 - Public network check: Click **Add Public Network Servers to Access This Instance**.
4. Click **Start Check** and a check report will be generated after the check is completed.
5. Locate the causes based on the report, solve the issues by following the handling suggestions, and connect again.
   - Check items and corresponding solutions in the private network check are as follows:
<table>
<thead><tr><th>Check Item</th><th>Exception Handling</th></tr></thead>
<tbody><tr>
<td>MySQL instance status</td>
<td>The MySQL instance has been terminated. If it is terminated by mistake, go to the <a href="https://console.cloud.tencent.com/mysql/recycle">recycle bin</a> to restore it.</td></tr>
<tr>
<td rowspan=2>CVM instance status</td>
<td>The CVM instance has been terminated. If it is terminated by mistake, go to the <a href="https://console.cloud.tencent.com/cvm/recycler/cvm">recycle bin</a> to restore it.</td></tr>
<tr>
<td>The CVM instance is shut down. To use it, start it up in the <a href="https://console.cloud.tencent.com/cvm/instance">CVM console</a>.</td></tr>
<tr>
<td rowspan=2>CVM and MySQL are in the same VPC</td>
<td>The network types of the CVM and MySQL instances are different. To make them in the same type of network, see <a href="#wlwt">Solutions to network issues</a> to modify their network types.</td></tr>
<tr>
<td>The CVM and MySQL instances are using different VPC IP ranges. To make them in the same VPC of the same region, see <a href="#wlwt">Solutions to network issues</a> to modify their VPCs.</td></tr>
<tr>
<td>CVM security group policy</td>
<td>The <strong>outbound rule</strong> of the CVM instance's security group rejects the access to the IP and port of the MySQL instance. To allow the access to the IP and port of the MySQL instance, see <a href="#caqzpzyw">Incorrect CVM security group configuration</a> to modify the outbound rule.</td></tr>
<tr>
<td>MySQL security group policy</td>
<td>The <strong>inbound rule</strong> of the MySQL instance's security group rejects the access from the IP and port of the CVM instance. To allow the access from the IP and port of the CVM instance, see <a href="#maqzpzyw">Incorrect MySQL security group configuration</a> to modify the inbound rule.</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/9af6e13c4dea0f77e49c9192026a0846.png">

   - Check items and corresponding solutions in the public network check are as follows:
<table>
<thead><tr><th>Check Item</th><th>Exception Handling</th></tr></thead>
<tbody><tr>
<td>MySQL instance status</td><td>The MySQL instance has been terminated. If it is terminated by mistake, go to the <a href="https://console.cloud.tencent.com/mysql/recycle">recycle bin</a> to restore it.</td></tr>
<tr>
<td>Public network access status</td>
<td>The public network access has been disabled for the MySQL instance. To enable it, see <a href="https://www.tencentcloud.com/document/product/236/37788">Connecting to MySQL Instance</a>.</td></tr>
</tbody></table>
<img src="https://qcloudimg.tencent-cloud.cn/raw/def8a3aa846e5ef72efd4d27adc06fe0.png">

#### [Step 2. If the causes cannot be located by the one-click connectivity checker, refer to the following reasons to check](id:step2)
[**Incorrect password**](id:mmwt)
If the connection password is incorrect, you can [reset the password](https://www.tencentcloud.com/document/product/236/31901) or [create a temporary account with sufficient permissions](https://www.tencentcloud.com/document/product/236/31900) to log in to the database.

[**Incorrect connection command syntax**](id:ljyfwt)
Check whether the connection command is correct according to the command syntax: `mysql -h hostname -u username -p` for private network connection and `mysql -h hostname -P port -u username -p` for public network connection. For more information, see [Connecting to MySQL Instance](https://www.tencentcloud.com/document/product/236/37788).

[**Incorrect IP and port in commands or configuration files**](id:idyw)
Check whether the IP and port displayed in the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) are consistent with those in commands and configuration files.

[**Incorrect database account permissions**](id:sjkzhzjpzyw)
Besides security groups, subnets, and other network configurations, database accounts control the access to MySQL. If a database account only allows some specific host addresses to access MySQL, the access from other host addresses will be rejected.
You can modify the host addresses authorized by a database account in the console to control the access to MySQL, thus enhancing database connection security.
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list, and enter the instance management page.
2. Select **Database Management** > **Account Management**, find the account for which to modify the host, and select **More** > **Modify Host** in the **Operation** column.
3. In the pop-up dialog box, enter the new host address and click **OK**.
>?The host address can be an IP and contain `%` (indicating no limit on the IP range). Multiple hosts should be separated by line breaks, spaces, semicolons, commas, or vertical bars.
>- Example 1: Enter `%` to indicate no limit on the IP range, that is, clients at all IP addresses are allowed to use this account to connect to the database.
>- Example 2: Enter `10.5.10.%` to indicate that clients with an IP range within `10.5.10.%` are allowed to use this account to connect to the database.

### [Symptom 3: Troubleshooting the DMC connection issues](id:dptdlsbclff)
1. Confirm that the database account has authorized all IPs of DMC servers in the region. For more information on authorization, see [Modifying Host Addresses with Access Permissions](https://intl.cloud.tencent.com/document/product/236/31903). You can also set **%** as the host address authorized by the database account to allow all IPs and only use security groups to control database access.
2. If you confirm that all needed IPs are authorized, then the cause may be incorrect password. Accordingly, you can enter the password again, reset the password, or create a temporary account with sufficient permissions. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/236/31901) and [Creating Account](https://intl.cloud.tencent.com/document/product/236/31900).

## Appendix 1
### [Solutions to network issues](id:wlwt)
If the networks of a CVM instance and a TencentDB for MySQL instance are of different types, the former cannot access the latter directly over the private network.

#### [CVM in a VPC but MySQL in the classic network](id:cvmj)
- **Solution 1 (recommended)**: Switch the TencentDB for MySQL instance from classic network to VPC as instructed in [Network Switch](https://www.tencentcloud.com/document/product/236/31915).
>!
>- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- The switch from classic network to VPC is irreversible.
>- Switching the network may cause the change of instance's private IP. The original IP will become invalid after the valid period has elapsed. Modify the instance IP on the client promptly.
>  The default valid period of the original IP is 24 hours and the longest valid period can be 168 hours. If the valid period is set to 0 hours, the original IP address will be released immediately after the network switch.
>- The switch from classic network to VPC is irreversible. After the switch to a VPC, the TencentDB instance cannot communicate with Tencent Cloud services in another VPC or classic network.
>- The network switch of a primary instance doesn't apply to its associated read-only instances or disaster recovery instances, you need to manually switch the network for these instances.
- **Solution 2**: Purchase a new CVM instance that resides in the classic network (the existing CVM instance cannot be migrated from VPC to classic network). However, VPC is more secure than classic network and thus highly recommended.
- **Solution 3**: Connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, so we recommend that you use VPC.

#### [CVM in the classic network but MySQL in a VPC](id:cjmv)
- **Solution 1 (recommended)**: Switch the CVM instance from classic network to VPC as instructed in [Switching to VPC](https://www.tencentcloud.com/document/product/213/20278).
>!  
>- After the switch, both instances must reside in the same VPC before they can interconnect over the private network.
>- You need to unbind private/public network CLB instances and ENIs and release auxiliary IPs of the primary ENI before migration and bind them again after migration.
>- The CVM instance will be restarted during migration. Do not perform other operations on it.
>- Check the instance status after migration and verify whether private network access and remote login work properly.
>- The switch from classic network to VPC is irreversible. After the switch, the CVM instance cannot communicate with Tencent Cloud services in the classic network.
- Solution 2: [Use Classiclink](https://intl.cloud.tencent.com/document/product/215/41419).
- **Solution 3**: Connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, so we recommend that you use VPC.

#### [CVM and MySQL in the same region but different VPCs](id:cmvbt)
By default, the CVM and TencentDB for MySQL instances can interconnect over the private network only if they are in the same VPC. If they are in the same region but different VPCs, interconnection over the private network can be achieved in the following ways.
- **Solution 1 (recommended)**: Migrate the MySQL instance to the same VPC as the CVM instance as instructed in [Network Switch](https://www.tencentcloud.com/document/product/236/31915).
- **Solution 2**: Create a [Cloud Connect Network](https://www.tencentcloud.com/zh/document/product/1003) between the two VPCs.
  Otherwise, the instances can only interconnect over the public network, which has poor performance, security, and stability.

#### [CVM and MySQL in different regions and different VPCs](id:dywt)
If the CVM and MySQL instances are in different regions and different VPCs, the former cannot access the latter directly over the private network.
- **Solution 1 (recommended)**: Use a CVM instance in the same VPC as the TencentDB for MySQL instance to connect.
- **Solution 2**: Create a [Cloud Connect Network](https://www.tencentcloud.com/zh/document/product/1003) between the two VPCs.
- **Solution 3**: Connect the CVM instance to the public network address of the TencentDB for MySQL instance. This solution has poor performance, security, and stability, so we recommend that you use VPC.

### [Solutions to security group configuration issues](id:aqzpzwt)
If the security groups of the CVM and MySQL instances are incorrectly configured, the former cannot access the latter directly over the private or public network.

#### [Incorrect CVM security group configuration](id:caqzpzyw)
To use the CVM instance to access the MySQL instance, you need to configure an outbound rule in the security group of the CVM instance. **If the target of the outbound rule isn't "0.0.0.0/0" and the protocol port isn't "ALL"**, the IP and port of the MySQL instance should be added to the rule.

1. Go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM console and click the name of the CVM-bound security group to enter its details page.
2. On the **Outbound rule** tab, click **Add Rule**.
Select **MySQL(3306)** as **Type**, enter your TencentDB for MySQL IP address (range) in **Target**, and select **Allow** for **Policy**.

#### [Incorrect MySQL security group configuration](id:maqzpzyw)
To use the CVM instance to access the MySQL instance, you need to configure an inbound rule in the security group of the MySQL instance. **If the source of the inbound rule isn't "0.0.0.0/0" and the protocol port isn't "ALL"**, the IP and port of the CVM instance should be added to the rule. 

1. Go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page in the CVM console and click the name of the TencentDB for MySQL-bound security group to enter its details page.
2. On the **Inbound rule** tab, click **Add Rule**.
Enter the allowed IP address (or range) and port and select **Allow**.
Select **MySQL(3306)** as **Type**, enter your CVM IP address (range) in **Source**, and select **Allow** for **Policy**.
>!To connect to a TencentDB for MySQL instance, you must open its port.
>- TencentDB for MySQL uses private network port 3306 by default and supports customizing the port. If the default port is changed, the new port should be opened in the security group.
>- The TencentDB for MySQL public port is automatically assigned by the system and cannot be customized. After the public network access is enabled, it will be controlled by the ACL of the security group. When configuring the security policy, you need to open the private port. You can log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID to enter the instance details page.
  ![](https://main.qcloudimg.com/raw/9f471c644eb9a5aa86bd092fdebd0255.png)

## Appendix 2
### [Viewing private and public network addresses](id:nwwpdff)
Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb), click an instance ID in the instance list to enter the instance details page, and view private and public network addresses.
![](https://main.qcloudimg.com/raw/322c89b12772441c4fd8e83f597092ed.png)

### [Viewing network type and VPC information](id:wllxvpdff)
To enable connection between CVM and TencentDB for MySQL instances over the private network, they must be under the same account and in the same VPC in the same region, or both in the classic network.
>?CVM and TencentDB for MySQL instances must be under the same account:
>- If the **Network** fields in the instance lists both show **Classic Network** or **VPC**, it means that the networks of the CVM and TencentDB for MySQL instances are of the same type.
>- If the **Network** fields in the instance lists both show the same **VPC** (in the same region), it means that the CVM and TencentDB for MySQL instances are in the same VPC.
>
- **View the network type/VPC of CVM**: Log in to the [CVM console](https://console.cloud.tencent.com/cvm/instance) and view network information in the instance list.
  ![](https://main.qcloudimg.com/raw/ce2550045bc286172f841f4fcceb0cc4.png)
- **View TencentDB for MySQL network type/VPC**: Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and view **Network** in the instance list.
  ![](https://main.qcloudimg.com/raw/2cc5396f1b3f8af2028d75ae642a5126.png)

