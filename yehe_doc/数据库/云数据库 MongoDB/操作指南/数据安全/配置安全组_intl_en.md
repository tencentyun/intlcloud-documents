You can configure a security group in the TencentDB for MongoDB console to control the outbound/inbound traffic.

## Background
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For specific rules and limitations, see [Overview](https://intl.cloud.tencent.com/document/product/215/38750).

>!
>- TencentDB security groups currently only support network access control for VPCs but not the classic network.
> - As TencentDB doesn't have any active outbound traffic, outbound rules don't apply to it.
>- TencentDB for MongoDB security groups support primary instances, read-only instances, and disaster recovery instances.
>- TencentDB for MongoDB supports the security group feature which is implemented based on the allowlist. To use this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Directions
### Step 1. Create a security group
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region above the instance list on the right, and click **Create**.
3. In the pop-up window, set the following configuration items, confirm that everything is correct, and click **OK**.
   - **Template**: Select a security group template in the drop-down list.
     - **Open all ports**: All ports are opened to the public and private networks. This may present security issues. Security group rules are added by default. You can click a security group template below to view its **Outbound Rules* and **Inbound Rules**.
     - **Open ports 22, 80, 443, and 3389 and the ICMP protocol**: Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network. Security group rules are added by default. The port of TencentDB for MongoDB is 27017 by default. You can ignore this template.
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
   - **Protocol Port**: Enter the protocol type and port for the client to access TencentDB for MongoDB. You can view the port information in the **Private Network Address** column in the [instance list](https://console.cloud.tencent.com/mongodb). The default port is 27017.
   - **Policy**: **Allow** or **Reject**. **Allow** is selected by default.
     - **Allow**: Traffic to this port is allowed.
     - **Reject**: Data packets will be discarded without any response.
   - **Notes**: A short description of the rule for easier management.
5. Click **Complete**.
   
### Step 3. Bind the security group to an instance
>!Currently, security groups can be configured only for TencentDB for MongoDB instances in VPC.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **More** > **Security Group**.
You can also click the target instance name, select the **Data Security** tab, and click **Configure Security Group**.
6. In the **Configure Security Group** pop-up window, select the target security group and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/6e9a53e1c4131f4c73a84af2213cfde9.png)

## More Operations
### Adjusting the priority of a bound security group
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID, select the **Data Security** tab, and view all security groups of the instance.
6. Click **Edit**. You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/b407f850a15a1362a1ac89a4b13ce955.png" style="zoom: 80%;" /> or <img src="https://qcloudimg.tencent-cloud.cn/raw/3efb762c31ec14fa16813748183eb520.png" style="zoom:80%;" /> in the **Operation** column to adjust the filtering priorities of security groups.
7. Click **Save**.

### Adjusting an inbound/outbound rule
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID, select the **Data Security** tab, and view all security groups of the instance.
6. In the security group list, click the target **security group ID** or name to enter the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page.
7. Find the security group rule to be modified and click **Edit** in the **Operation** column to edit it.

### Importing a security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click the ID/name of a security group.
2. On the **Inbound Rule** or **Outbound Rule** tab, click **Import Rule**.
3. In the pop-up window, select an edited inbound/outbound rule template file and click **Import**.
>? 
>- As existing rules will be overwritten after importing, we recommend you export the existing rules before importing new ones.
>- If there are no existing rules in the security group, download a template and edit it before importing it.

### Cloning a security group
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the target security group and click **More** > **Clone** in the **Operation** column.
2. In the pop-up window, select the target region and project and click **OK**.
If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

### Deleting a security group
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the security group to be deleted and click **More** > **Delete** in the **Operation** column.
2. In the pop-up window, click **OK**.
If the current security group is associated with a CVM instance, it must be disassociated first before it can be deleted.

## References
For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).

