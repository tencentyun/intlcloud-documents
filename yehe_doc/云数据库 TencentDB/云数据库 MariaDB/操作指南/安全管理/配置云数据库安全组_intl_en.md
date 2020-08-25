Security group serves as a stateful virtual firewall with filtering feature for configuring network access control for one or more TencentDB instances. It is an important network security isolation tool provided by Tencent Cloud.
Instances in VPC with the same network security isolation demands in one region can be put into the same security group, which is a logical group (not supported for instances in the classic network currently). TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. Rules not supported by TencentDB will not take effect.
>!TencentDB security group currently only supports network access control for VPCs but not the classic network or the public network.

## TencentDB Security Group Management
1. Log in to the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql), click an instance name in the instance list to enter the instance management page.
2. Select **Data Security** > **Security Group** to manage TencentDB security groups.
>!
> 1. TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the TencentDB security group management page.
> 2. You cannot create or delete security group rules on the TencentDB security group management page.

## Security Group Policy
Security group policies are divided into "allowing" and "rejecting" traffic. You can configure security group rules to allow or reject inbound traffic of instances deployed in VPC.

## Default Policy of a TencentDB Security Group
Currently, if you select VPC as the network type when purchasing a TencentDB instance, there is no need to associate a security group. In this case, the default policy is to "open all IPs and ports to Internet".

## Security Group Templates
You can create a custom security group, or create a security group from a template. You can control the inbound and outbound packets of CVMs by configuring security group rules.
All ports opened: the access to TencentDB from all IP addresses is allowed, which comes with certain security risks. Please use this template with caution.

## Security Group Rules
Security group rules are used to control the inbound and outbound traffic of instances associated with the security group (filtered based on the rules from top to bottom). By default, a new security group rejects all traffic (All Drop). You can modify security group rules at any time, and the new rules take effect immediately.
Each security group rule involves the following items:
- Protocol port: for TencentDB, only **ALL** is supported for protocol port. As TencentDB only provides access over fixed ports, there is no need to specify a port. If a port is specified, the rule will not take effect for TencentDB.
- Authorization type: access based on address ranges (CIDR/IP).
- Source (inbound rules) or target (outbound rules): choose one of the following options:
    - Specify a single IP in CIDR notation.
    - Specify an IP address range in CIDR notation, such as 203.0.113.0/24.
- Policy: allow or reject the access request.

## Security Group Priority
You can set security group priority in the TencentDB console, and the smaller the number, the higher the priority. If an instance is associated with multiple security groups, the priority is used as a basis for evaluating the security rules for this instance.
In addition, if the last policy in multiple security groups associated with an instance is **ALL Traffic Denied**, then the last policy **ALL Traffic Denied** of all security groups except the one with the lowest priority will not take effect.

## Security Group Restrictions
- Security groups apply to TencentDB instances in VPC [Network Environment](/doc/product/213/5227).
- Each user can configure a maximum of 50 security groups for each project in a region.
- A maximum of 100 inbound or outbound rules can be configured for a security group. As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
- A TencentDB instance can be associated with multiple security groups, and a security group can be associated with multiple TencentDB instances. No limit is imposed on the number.

>!We do not recommend associating too many instances with a security group, although no limit is imposed on the number of instances.

| Feature | Quantity |
|---------|---------|
| Security group | 50/region |
| Access policy | 100 (inbound/outbound) |
| Number of security groups associated with an instance | No limit |
| Number of instances associated with a security group | No limit |

## Creating, Managing, and Deleting Security Group Rules
TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the TencentDB security group management page.
To create, manage, or delete security group rules, please do so on the [security group management page](https://console.cloud.tencent.com/cvm/securitygroup).
