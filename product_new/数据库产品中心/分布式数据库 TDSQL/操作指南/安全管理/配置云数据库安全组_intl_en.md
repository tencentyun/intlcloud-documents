A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. VPC-based instances with identical network security isolation requirements in the same region can be put into the same logical security group. This feature is currently not supported for instances on the basic network. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. Rules that are not supported by TencentDB become invalid automatically.

>
>- TencentDB security group currently only supports network access control over private and public network access in VPCs but not over the basic network.
> - Security groups that currently support public network access are available only in Guangzhou, Shanghai, Beijing, and Chengdu.

## Managing TencentDB security groups
Log in to the [TDSQL Console](https://console.cloud.tencent.com/dcdb), click an instance name in the instance list to enter the management page, and select **Data Security** > **Security Group** to manage security groups.
>
>- TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the TencentDB security group management page.
>- You cannot create or delete security group rules on the TencentDB security group management page.
> 
![](https://main.qcloudimg.com/raw/29be2ecacf26245b65ef45e703b910de.png)

## Security group policy
Security group policies are divided into "allowing" and "denying" traffic. You can use a security group policy to filter the inbound traffic of an instance, which can be a **VPC-based TencentDB instance**.

## Default policy of a TencentDB security group
Currently, if you select VPC as the network type when purchasing a TencentDB instance, there is no need to associate a security group. In this case, the default policy is to "open all IPs and ports to internet".

## Security group template
You can create a custom security group or create one from template. You can control the inbound and outbound packets on CVM instances by configuring security group rules. Three templates are currently available in the system:
- Port 22 opened on Linux: Only TCP port 22 for SSH logins is opened to the public network, while all ports are opened to the private network. This template is not applicable to TencentDB.
- Port 3389 opened on Windows: Only TCP 3389 for MSTSC logins is opened to the public network, while all ports are opened to the private network. This template is not applicable to TencentDB.
- All ports opened: Access to TencentDB from all IP addresses is allowed, which comes with certain security risks.

## Security group rules
Security group rules are used to control the inbound and outbound traffic on instances associated with the security group (filtered based on the rules from top to bottom). By default, a new security group denies all traffic (All Drop). You can modify security group rules at any time, and new rules take effect immediately once saved.
Each security group rule involves the following items:
- Protocol port: For TencentDB, only **ALL** is supported for protocol port. As TencentDB only provides access over fixed ports, there is no need to specify a port. If a port is specified, the rule will not take effect for TencentDB.
- Authorization type: Access based on address ranges (CIDR/IP).
- Source (inbound rules) or destination (outbound rules): Choose one of the following options:
    - Specify a single IP in CIDR notation.
    - Specify an IP range in CIDR notation.
- Policy: Allow or Deny.

## Security group priority
You can set security group priority in the instance console. The smaller the number, the higher the priority. If an instance is bound to multiple security groups, the priority will be used as the basis for determining the overall security rules of the instance.
In addition, if the last policy of such security groups is "ALL Traffic denied", then the last policy in each of them, except the one with the lowest priority, will become invalid.

## Security group restrictions
- Security groups are applicable to TencentDB instances in [VPC](/doc/product/213/5227).
- Each user can set up to 50 security groups under the same project in the same region.
- A maximum of 100 inbound and 100 outbound access policies can be set in one security group. As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
- A TencentDB instance can be associated with multiple security groups, and a security group can be associated with multiple TencentDB instances. No limit is imposed on the number.

>It is not recommended to associate too many instances with a security group.

| Feature | Quantity | 
|---------|---------|
| Security group | 50/region |
| Access policy | 100 inbound ones, 100 outbound ones |
| Number of security groups associated with an instance | Unlimited |
| Number of instances associated with a security group | Unlimited |

## Creating, managing, and deleting security group rules
TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the TencentDB security group management page. To create, manage, and delete security group rules, you should go to the [security group management page](https://console.cloud.tencent.com/cvm/securitygroup).
