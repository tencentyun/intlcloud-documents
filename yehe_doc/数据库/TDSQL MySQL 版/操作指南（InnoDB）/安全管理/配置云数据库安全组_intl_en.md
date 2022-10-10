A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances in VPC with the same network security isolation demands in one region can be put into the same security group, which is a logical group (not supported for instances in the classic network currently). TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. Rules not supported by TencentDB will not take effect.

>?TencentDB security groups provide network access control for VPCs, and support public network access for the instances with public network access enabled in Guangzhou, Chengdu, Shanghai, Beijing, and Nanjing regions.

## TencentDB Security Group Management
Log in to the [TDSQL for MySQL console](https://console.cloud.tencent.com/dcdb), click an instance ID in the instance list to enter the management page, and select **Data Security** > **Security Group** to manage security groups.
>!
>- TencentDB shares the security group rules of CVM. You can match or adjust the rule priority as needed on the TencentDB security group management page.
>- You cannot create or delete security group rules on the TencentDB security group management page. For details, see [Viewing a Security Group](https://intl.cloud.tencent.com/document/product/215/35507).
> 
![](https://main.qcloudimg.com/raw/29be2ecacf26245b65ef45e703b910de.png)

## Security Group Policy
Security group policies are divided into "allowing" and "rejecting" traffic. You can configure security group rules to allow or reject inbound traffic of instances deployed in VPC.

## Default Policy of a TencentDB Security Group
Currently, if you select VPC as the network type when purchasing a TencentDB instance, there is no need to associate a security group. In this case, the default policy is to "open all IPs and ports to internet".

## Security Group Templates
You can create a security group from scratch or from a template, and control the inbound and outbound packets of CVMs by configuring rules for the security group.

## Security Group Rules
Security group rules are used to control the inbound and outbound traffic of instances associated with the security group (filtered based on the rules from top to bottom). By default, a new security group rejects all traffic (All Drop). You can modify security group rules at any time, and the new rules take effect immediately.
Each security group rule contains the following items:
- Protocol and port: As TencentDB only provides access over fixed ports, security group rules configured with other ports won't take effect for TencentDB. For example, if the TencentDB instance uses port 3306 for access, you can configure `TCP:3306` or `ALL` in the security group rule.
- Authorization type: Access based on address ranges (CIDR/IP).
- Source (inbound rules) or target (outbound rules): Choose one of the following options:
    - Specify a single IP in CIDR notation.
    - Specify a single IP in CIDR notation.
- Policy: Allow or reject the access request.

## Security Group Priority
You can set security group priority in the TencentDB console, and the smaller the number, the higher the priority. If an instance is associated with multiple security groups, the priority is used to evaluate the security rules for the instance.
In addition, if the last policy in multiple security groups associated with an instance is **ALL Traffic Denied**, then the last policy **ALL Traffic Denied** of all security groups except the one with the lowest priority will not take effect.

## Security Group Restrictions
- Security groups are applicable to TencentDB instances in [VPC](https://intl.cloud.tencent.com/document/product/213/5227).
The security group policy is only valid for the private IP. Enable the database public network access with CVM to ensure the best security for the business.
- Each user can set up to 50 security groups under the same project in the same region.
- A maximum of 100 inbound or outbound rules can be configured for a security group. As TencentDB doesn’t have any active outbound traffic, outbound rules don’t apply to it.
- A TencentDB instance can be associated with multiple security groups, and a security group can be associated with multiple TencentDB instances. No limit is imposed on the number.

>!We do not recommend associating too many instances with a security group, although no limit is imposed on the number of instances.

| Feature | Quantity |
|---------|---------|
| Security group | 50/region |
| Access policy | 100 (inbound/outbound) |
| Number of security groups associated with an instance | No limit |
| Number of instances associated with a security group | No limit |

## Creating/Managing/Deleting Security Group Rules
To create, manage, and delete security group rules, you can go to the [Security Group] page (https://console.cloud.tencent.com/cvm/securitygroup). For details, see [Viewing a Security Group](https://intl.cloud.tencent.com/document/product/215/35507).
