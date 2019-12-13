## Operation Scenario
A security group is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. 


>- TencentDB for MySQL security group currently only supports network access control for VPC and public networks but not basic networks.
> - Security groups that currently support public network access are available only in Guangzhou, Shanghai, Beijing, and Chengdu.
> - As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
> - TencentDB for MySQL security groups support master instances, read-only instances, and disaster recovery instances.


## Directions
### Creating a Security Group
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar and click **Create**.
3. In the pop-up dialog box, select or customize a template in **Template**, enter the security group **name** (such as my-security-group), select a **project**, enter **remarks** (optional), and then click **OK**.
>
 - Port 22 opened on Linux: Only TCP port 22 for SSH logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
 - Port 3389 opened on Windows: Only TCP 3389 for MSTSC logins is opened to the public network, while all ports are opened to the private network. **This template is not applicable to TencentDB.**
 - All ports opened: Access to TencentDB from all IP addresses is allowed, which comes with certain security risks.
>
![](https://main.qcloudimg.com/raw/5ff13000731c0ccf9904dda884df7478.png)

### Configuring a Security Group for TencentDB
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is an instance-level firewall provided by Tencent Cloud for controlling inbound/outbound traffic of TencentDB. You can associate a security group with an instance when purchasing it or later in the console.

>TencentDB for MySQL security groups currently only support the **VPC TencentDB** configuration.

1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance for which to configure a security group and click **Manage** in the "Action" column to enter the instance management page.
3. On the **Security Group** tab, click **Configure a Security Group**.
4. In the pop-up dialog box, select the security group to be bound and click **OK**. 
![](https://main.qcloudimg.com/raw/b836f83d5a20b91e588a4d4b3528f263.png)

### Deleting a Security Group
1. Log in to the CVM Console and go to the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page.
2. Select the security group to be deleted and select **More** > **Delete** in the "Action" column.
![](https://main.qcloudimg.com/raw/708d17dcd00d6ce4db06821f33cdaf7f.png)
3. Click **OK** in the pop-up dialog box. If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.

### Cloning a Security Group
1. Log in to the CVM Console and go to the security group page. Select **More** > **Clone** in the "Action" column.
2. In the pop-up dialog box, select the target region and target project and click **OK**. If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

### Adding Rules to a Security Group
1. Log in to the CVM Console and go to the security group page. Select the security group to be updated and click its ID/name to enter its details page where you can find tabs for inbound rules and outbound rules.
2. On the Inbound Rules or Outbound Rules tab, click **Add a Rule**.
![](https://main.qcloudimg.com/raw/73b31badbb00c384461e54566a90357f.png)
3. In the pop-up dialog box, enter the required information. For example, specify "0.0.0.0/0" for the source/destination, "TCP:3306" for the protocol port, and "Allow" for the policy, and then click **Finish**. You can click **New Line** to add more rules.
![](https://main.qcloudimg.com/raw/0efea06b87cb9f6d25a615c61acdf675.png)

### Importing/Exporting a Security Group Rule
1. Log in to the CVM Console and go to the security group page. Select the security group to be updated and click its ID/name to enter its details page where you can find tabs for inbound rules and outbound rules.
2. On the Inbound Rules or Outbound Rules tab, click **Import a Rule**.
![](https://main.qcloudimg.com/raw/3a7e52796c1b9a66295f557c694998ae.png)
3. If you already have a rule, you are recommended to export it first as importing a rule will overwrite the existing one. If no rule exists, export a template first, edit the template file, click **Select a File** in the pop-up dialog box to select the edited file, and click **Start Import**.	
![](https://main.qcloudimg.com/raw/98ecb63181c1357afc4b29b5ca9b87e3.png)


