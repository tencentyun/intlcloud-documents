## Overview
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For specific rules and limitations, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750). You can bind a security group directly during instance purchase or bind one in the console after instance purchase.

>?
>- TencentDB for Redis security groups currently only support network access control for VPCs and public networks but not the classic network.
> - As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
> - TencentDB for Redis security groups support master instances, read-only instances, and disaster recovery instances.

## Configuring Security Groups for TencentDB
### Step 1. Create a security group
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region above the instance list on the right, and click **Create**.
3. In the pop-up window, set the following configuration items, confirm that everything is correct, and click **OK**.
   - **Template**: Select a security group template in the drop-down list.
     - **Open all ports**: All ports are opened to the public and private networks. This may present security issues. Security group rules are added by default. You can click a security group template below to view its **Outbound Rules* and **Inbound Rules**.
     - **Open ports 22, 80, 443, and 3389 and the ICMP protocol**: Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network. Security group rules are added by default. The port of TencentDB for Redis is 6379 by default. You can ignore this template.
     - **Custom**: You can create a security group and then add custom rules.
   - **Name**: Custom name of the security group.
   - **Project**: Select a project for easier management. By default, **Default Project** is selected.
   - **Notes**: A short description of the security group for easier management.
   - **Advanced Configuration**: You can add tags for the security group.
4. If you select **Custom** for **Template**, click **Set Now** in the **Note** window and perform the following steps.

### [Step 2. Set inbound rules in the security group](id:Step2)

1. On the **Inbound Rule** tab of the **Security Group Rules** page, click **Add Rules**.
2. In the **Add Inbound Rules** pop-up window, set the rules.
   - **Type**: Select **Custom** as the default type.
   - **Source**: Set the source for database access, i.e., the inbound source, in the following formats:
     <table>
     <tr><th>Source Format</th><th>Description</th></tr>
         <tr><td>CIDR notation</td>
             <td><ul><li>A single IPv4 address or an IPv4 range in CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</li><li>A single IPv6 address or an IPv6 range in CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</li></ul></td></tr>
     <tr>
         <td>Security group ID</ul>
     </td>
         <td>Reference a security group ID to match the IP address of the server associated with the security group.
     </td></tr>
     <tr>
         <td>Parameter template</td>
         <td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td></tr>
     </table>
   - **Protocol Port**: Enter the protocol type and port for the client to access TencentDB for Redis. You can view the port information in the **Private IPv4 Address** in the **Network Info** section on the [Instance Details](https://console.cloud.tencent.com/redis) page. The default port is 6379. If the access protocol is TCP, you can enter `TCP:6379`.
    - **Policy**: **Allow** or **Reject**. **Allow** is selected by default.
      - **Allow**: Access requests of this port are allowed.
      - **Reject**: Data packets will be discarded without any response.
    - **Notes**: A short description of the rule for easier management.
4. Click **Complete**.
   

### Step 3. Bind the security group to a database instance

>!Currently, security groups can be configured only for TencentDB for Redis instances in VPC.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the **Instance List** on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the instance management page.
5. On the **Security Group** tab, click **Configure Security Group**.
6. In the **Configure Security Group** pop-up window, select a created security group. You can filter security group by project name.
	 ![](https://qcloudimg.tencent-cloud.cn/raw/0c6baef3aba1234459172ac0e38610f6.png)
7. Click **OK**. 
   - In the **Associated Security Group** section, you can view the list of security groups associated with the database instance.
     - In the **Priority** column, you can view the priorities of security groups.
     - You can click a security group ID to enter the **Security Group Rules** page and edit the rules as instructed in [Modifying a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35515). For more operations, see [Viewing a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35514).
     - **Security Group Name**: The name of the security group is displayed for easier identification.
     - **Operation**: You can click **Edit** above the list and click ![img](https://qcloudimg.tencent-cloud.cn/raw/b407f850a15a1362a1ac89a4b13ce955.png) or ![img](https://qcloudimg.tencent-cloud.cn/raw/3efb762c31ec14fa16813748183eb520.png) to adjust the priority of the security group. You can also click <img src="https://qcloudimg.tencent-cloud.cn/raw/ef650a132e219e69f4792ce463e69fe0.png" style="zoom: 67%;" /> to delete the bound security group.
   - On the **Preview Rules** page, you can view the inbound source information of the security group on the **Inbound Rules** tab.
   ![](https://qcloudimg.tencent-cloud.cn/raw/f039fa18f820e1828164e150bf6d4351.png)

## More Operations

- For more security group operations, see [Viewing a Security Group](https://intl.cloud.tencent.com/document/product/215/35507).
- For more security group rule operations, see [Viewing a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35514).
- For security group APIs, see [DeleteSecurityGroup](https://intl.cloud.tencent.com/document/product/215/15803).
