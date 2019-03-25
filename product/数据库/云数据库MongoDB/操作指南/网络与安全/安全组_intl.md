## Scenarios
A security group serves as a stateful virtual firewall with filtering feature for setting network access control for one or more databases. It is an important network security isolation tool provided by Tencent Cloud. A security group is a logical group. You can associate the database instances with the same network security isolation requirements in the same region with the same security group. The databases share the security group list with the CVMs. Matching is performed based on the rules in the security group. See the detailed security group description for specific rules and limitations.

>!
> 1. Database security group **only supports the network control of private network access in VPCs, and does not support the network control of basic networks**.
> 2. **No outbound traffic is generated for databases, so outbound rules do not take effect for databases**.
> 3. TencentDB for MongoDB security group supports master instances, read-only instances and disaster recovery instances.
> 4. Notes for default security group templates:
>  - Port 22 opened on Linux: Only TCP port 22 for SSH login is exposed to Internet, and all private network ports are opened to Internet. **This template is unavailable for databases**.
>  - Port 3389 opened on Windows: Only TCP port 3389 for MSTSC login is exposed to Internet, and all private network ports are opened to Internet. **This template is unavailable for databases**.
>  - All ports opened to Internet: Allow all IPs to access databases. This involves a certain security risk.
> 5. The security group feature is implemented based on the whitelist. [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply for this feature.

## Procedure

### Create a security group

1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com/), and select **Products** -> **Cloud Virtual Machine** to go to the CVM management page.
2. Click **Security Groups** in the left navigation bar to enter the security group management page.
   ![](https://main.qcloudimg.com/raw/9c154ef45b104ffebef99a3de249b50c.png)
2. Click **Create**, select **Template** or **Custom**, and then enter the **Name** of the security group, such as my-security-group. Select **Project**, enter **Notes** (optional), and then click **OK**.
![](https://main.qcloudimg.com/raw/cc9a780ddd091f68c5476ee8463e1294.png)

### Configure security groups for TencentDB for MongoDB
[Security Group](https://cloud.tencent.com/doc/product/213/500) is an instance-level firewall provided by Tencent Cloud that is used to control inbound/outbound traffic of databases. You can associate a security group when you purchase an instance, or associate one in the console after you have purchased an instance.

> ! TencentDB for MongoDB security group is only available for **VPC-based databases**.

1. Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb), select the instance for which you want to configure security groups in the instance list, and click **Manage** -> **Security Groups** in the **Operation** column.
![](https://main.qcloudimg.com/raw/22337a8d71bb79228790c3253d4fd3e2.png)
2. Select the security group to be associated and click **OK** to associate the security group with TencentDB for MongoDB. 
![](https://main.qcloudimg.com/raw/b63568e07e679628d17d61b75fb453f5.png)

### Delete a security group
1. Log in to the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), and select **More** -> **Delete** in the **Operation** column of the security group list.
![](https://main.qcloudimg.com/raw/794d76f9f7969fe66f250b63e7a99415.png)
2. In the pop-up deletion confirmation box, click **OK**. If the security group is associated with a CVM, you need to remove the association before deleting the security group.

### Clone a security group
1. Log in to the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), and select **More** -> **Clone** in the **Operation** column of the security group list.
   ![](https://main.qcloudimg.com/raw/28810c1f2b863caac6d4598d3b4c5c07.png)
2. In the clone security group dialog box, select the target region and the target project, and click **OK**. If the new security group needs to be associated with CVMs, associate it with the desired CVMs.

### Add rules to a security group
1. Log in to the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select the security group you want to update, and click the security group ID to enter the details page, on which you can see the detailed information of the security group and the inbound/outbound rules.
2. On the **Inbound rule/Outbound rule** tab, click **Add a Rule**.
  ![](https://main.qcloudimg.com/raw/c2c4533dc6ff96e4f2af2fb8ee0fea30.png)
3. Select the options for the inbound/outbound rules, and enter the required information. For example, specify "10.0.0.0/0" for source/destination, "TCP:3306" for protocol port, and "Allow" for the policy, and then click **Completed**. You can click **New Line** to add more rules.
  ![](https://main.qcloudimg.com/raw/2f48931b61d45ab8275e12cf0cf70945.png)

### Import/Export security group rules
1. Log in to the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select the security group you want to update, and click the security group ID to enter the details page.
2. On the **Inbound rule/Outbound rule** tab, click **Import rule**.
![](https://main.qcloudimg.com/raw/ab01ffb53084acf3e88219df7aca7b25.png)
3. If a rule already exists in the security group, export the existing rule first, otherwise it will be overwritten by the imported rules. If no rule exists, you can export an template and edit it, then click **Selecting file...** to select the edited template file, and click **Import**.	
![](https://main.qcloudimg.com/raw/fda954cd9eaa9058a1fea6ca52d12f50.png)

