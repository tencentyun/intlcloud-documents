A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. **Instances in VPC** with the same network security isolation demands in one region can be put into the same security group, which is a logical group (not supported for instances in the basic network currently). TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. Rules not supported by TencentDB will not take effect.
>TencentDB security group currently only supports private network access to VPC but not network control for the basic network and public network access.


## TencentDB Security Group Management
In the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), select **Instance List** > **Data Security** > **Security Group** to manage TencentDB instances.

![](https://main.qcloudimg.com/raw/421d67b860892f10c536fc25c9d95d7c.png)

>**Note:**
> 1. TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the **TencentDB Security Group Management** page.
> 2. You cannot create or delete security group rules on the TencentDB Security Group Management page. 

## Security Group Policy
Security group policies are divided into "allowing" and "denying" traffic. You can use a security group policy to filter the inbound traffic of an instance, which can be a **VPC-based TencentDB** instance.

## Default Policy of a TencentDB Security Group

Currently, if you select VPC as the network type when purchasing a TencentDB instance, there is no need to associate a security group. In this case, the default policy is to "open all IPs and ports to internet".

## Security Group Template
You can create a custom security group or create a security group from template. You can control the inbound and outbound data packets of CVM instances by configuring security group rules. Three templates are available in the system currently:
- Port 22 opened on Linux: only TCP port 22 for SSH logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
- Port 3389 opened on Windows: only TCP 3389 for MSTSC logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
- All ports opened: the access to TencentDB from all IP addresses is allowed, which comes with certain security risks. Please use this template with caution.

## Security Group Rule
Security group rules are used to control the inbound and outbound traffic of instances associated with the security group (filtered by rule from top to bottom). By default, a new security group denies all traffic (All Drop). You can modify security group rules at any time, and new rules will take effect immediately once saved.
Each security group rule involves the following items:
- Protocol port: for TencentDB, only **ALL** is supported for protocol port. As TencentDB only provides access over fixed ports, there is no need to specify a port. If a port is specified, the rule will not take effect for TencentDB.
- Authorization type: access based on address range (CIDR/IP).
- Source (inbound rules) or target (outbound rules): choose one of the following options:
    - Specify a single IP in CIDR notation.
    - Specify an IP address range (such as 203.0.113.0/24) in CIDR notation.
- Policy: whether to allow or deny.

## Security Group Priority
You can set security group priority in the instance console. The smaller the number, the higher the priority. If an instance is associated with multiple security groups, the priority will be used as the basis for evaluating the overall security rules for this instance.
In addition, if the last policy in multiple security groups associated with an instance is **ALL Traffic Denied**, then the last policy **ALL Traffic Denied** of all security groups except the one with the lowest priority will not take effect.

## Security Group Restrictions

- Security groups are applicable to TencentDB instances in a VPC [network environment](/doc/product/213/5227).
- Each user can set up to 50 security groups for each project in a region.
- Up to 100 inbound and 100 outbound access policies can be set in a security group. **As no outbound traffic is generated for TencentDB instances, outbound rules do not take effect for TencentDB**.
- One TencentDB instance can be added to multiple security groups, and one security group can be associated with multiple TencentDB instances. No limit is imposed on the quantity.

>Although no limit is imposed on the quantity, you are not recommended to add too many instances to a security group.

| Feature Description | Quantity | 
|---------|---------|
| Security group | 50/region |
| Access policy | 100 for inbound access and 100 for outbound access |
| Security groups associated with an instance | Unlimited |
| Instances added to a security group | Unlimited |

## Creating, Managing, and Deleting Security Group Rules
TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the **TencentDB Security Group Management** page. To create, manage, or delete security group rules, please do so on the [security group management page](https://console.cloud.tencent.com/cvm/securitygroup).
