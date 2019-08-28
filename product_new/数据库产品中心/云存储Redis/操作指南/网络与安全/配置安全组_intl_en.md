
## Scenario
A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. 
>
> - TencentDB security group currently **only supports network access control for VPC and public networks, but not basic networks**.
> - Security groups that currently support **public network access** are available only in Guangzhou, Shanghai, Beijing, and Chengdu.
> - **As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB**.
> - TencentDB for Redis security group supports the master instance, read-only instances, and disaster recovery instances.
> - Templates are provided for security groups by default. Please take note that:
 - Port 22 opened on Linux: Only TCP port 22 for SSH logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
 - Port 3389 opened on Windows: Only TCP 3389 for MSTSC logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
 - All ports opened: Access to TencentDB from all IP addresses is allowed, which comes with certain security risks.


## Directions
### Creating a Security Group

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), click **Cloud Virtual Machine** to enter the CVM management page, and click **Security Group** on the left sidebar to enter the security group management page.
![](https://main.qcloudimg.com/raw/f0c0af30036ba512b9ef95f7d3991b82.png)
2. Click **Create**, select or customize a template in **Template**, enter the security group **name** (such as my-security-group), select a **project**, enter **remarks** (optional), and then click **OK**.


### Configuring A Security Group
[Security Group](https://cloud.tencent.com/doc/product/213/500) is an instance-level firewall provided by Tencent Cloud that is used to control inbound/outbound traffic of databases. You can associate a security group when you purchase an instance or associate one in the console after purchasing an instance.
> TencentDB for Redis security group currently only supports the **VPC TencentDB** configuration.

1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis).
2. In the instance list, select the instance for which to configure a security group, and click the instance name to enter the instance details page.
3. On the **Security Group** tab, click **Configure Security Group**.
![](https://main.qcloudimg.com/raw/bc4c29cc41e8633f9e93296f4b812142.png)
4. Select the security group to be bound and click **OK** to bind the security group to TencentDB. 

### Deleting a Security Group
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and select **More** > **Delete** in the **Operation** column.
2. On the security group deleting page, click **OK**.
> If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.

### Cloning a Security Group
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and select **More** > **Clone** in the **Operation** column.
2. On the security group cloning page, select the destination region and destination project, and click **OK**.
> If the new security group needs to be associated with a CVM instance, do so in the "Manage Instance" section of the security group.

### Creating a Security Group Rule
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and click the name of the security group to be updated.
2. On the **Inbound/Outbound Rules** page, click **Create a Rule**.
3. On the rule creating page, configure the rule information. For example, specify the source/destination as 10.0.0.0/0 and the protocol port as TCP:3306 and click **Complete**.

### Importing/Exporting a Security Group Rule
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/cvm/securitygroup) and click the name of the select the security group to be updated.
2. On the **Inbound/Outbound Rules** page, click **Import Rule**.
 - If you already have a rule, you are recommended to export it first as importing a rule will overwrite the existing one.
 - If the existing rule is empty, first export the template, edit the template file, click **Select a Template** to select it, and then click **Start Import**.	





