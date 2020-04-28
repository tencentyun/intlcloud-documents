
## Operation Scenarios
A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list.
>
> - TencentDB security group currently only supports network access control for VPCs and public network but not the basic network.
> - Security groups that currently support public network access are available only in Guangzhou, Shanghai, Beijing, and Chengdu.
> - As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
> - TencentDB for Redis security group supports master, read-only, and disaster recovery instances.
> - Templates are provided for security groups by default. Please take note that:
 - Port 22 opened on Linux: only TCP port 22 for SSH logins is opened to the public network, while all ports are opened to the private network. This template is not applicable to TencentDB.
 - Port 3389 opened on Windows: only TCP 3389 for MSTSC logins is opened to the public network, while all ports are opened to the private network. This template is not applicable to TencentDB.
 - All ports opened: access to TencentDB from all IP addresses is allowed, which comes with certain security risks.


## Directions
### Creating security group
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/securitygroup) and select **Security Group** on the left sidebar.
2. Click **Create**, select or customize a template in **Template**, enter the security group **name** (such as my-security-group), select a **project**, enter **remarks** (optional), and then click **OK**.

### Configuring security group
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is an instance-level firewall provided by Tencent Cloud for controlling inbound/outbound traffic of TencentDB. You can associate a security group with an instance when purchasing it or later in the console.
> Currently, security groups can be configured only for TencentDB for Redis instances in VPC.

1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and click an instance name in the instance list to enter the instance management page.
2. On the **Security Group** tab, click **Configure Security Group**.
3. In the pop-up dialog box, select the security group to be bound and click **OK**. 

### Deleting security group
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and select **More** > **Delete** in the "Operation" column.
2. In the pop-up dialog box, click **OK**.
>If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.

### Cloning security group
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and select **More** > **Clone** in the "Operation" column.
2. In the pop-up dialog box, select the target region and target project and click **OK**.
>If the new security group needs to be associated with a CVM instance, do so in the "Manage Instance" section of the security group.

### Adding security group rule
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and click the name of the security group to be updated.
2. On the **Inbound/Outbound Rules** page, click **Add Rule**.
3. In the pop-up dialog box, configure the rule information. For example, specify the source/destination as 10.0.0.0/0 and the protocol port as TCP:3306 and click **Complete**.

### Importing/Exporting security group rule
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and click the name of the security group to be updated.
2. On the **Inbound/Outbound Rules** page, click **Import Rule**.
 - If you already have a rule, you are recommended to export it first as importing a rule will overwrite the existing one.
 - If the existing rule is empty, first export the template, edit the template file, click **Select File** to select it, and then click **Start Import**.	

