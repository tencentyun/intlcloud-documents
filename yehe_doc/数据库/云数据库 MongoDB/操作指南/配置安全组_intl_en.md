You can configure a security group in the TencentDB for MongoDB console to control the outbound/inbound traffic.

## Background
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For specific rules and limitations, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750).

>!
>- TencentDB security groups currently only support network access control for VPCs but not the classic network.
>- As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
>- TencentDB for MongoDB security groups support primary instances, read-only instances, and disaster recovery instances.
>- TencentDB for MongoDB supports the security group feature which is implemented based on the allowlist. To use this feature, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## Directions
### Step 1. Create a security group
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region above the instance list on the right, and click **Create**.
3. In the **Create Security Group** pop-up window, set the following configuration items and click **OK**.
   - **Template**: select a template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
<tr><th>Template</th><th>Description</th><th>Remarks</th></tr>
<tr><td>Open all ports</td><td>All ports are opened to the public and private networks. This may present security issues.</td><td>-</td></tr>
<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This template does not take effect for TencentDB.</td></tr>
<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, see "Step 2. Add a security group rule"</a> below.</td><td>-</rd></tr>
</table>
   - **Name**: name of the security group.
   - **Project**: select a project for easier management. By default, **Default Project** is selected.
   - **Remarks**: a short description of the security group for easier management.
4. Select **Advanced Settings**, and you can set tags for the security group.

### [Step 2. Add a security group rule](id:Step2)
1. In the security group list on the [security group](https://console.cloud.tencent.com/cvm/securitygroup) page, search for the target security group in the search box in the top-right corner.
2. Find the target security group and click **Modify Rule** in the **Operation** column.
3. On the **Inbound Rule** tab of the **Security Group Rules** page, click **Add Rule**.
4. In the **Add Inbound Rule** pop-up window, set the rule.
   - **Type**: **Custom** is selected by default. You can also choose another system rule template.
   - **Source** or **Target**: traffic source (inbound rules) or target (outbound rules). You need to specify one of the following options:
<table>
<tr><th>Source or Target</th><th>Description</th></tr>
<tr>
<td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
<tr>
<td>A single IPv6 address or an IPv6 range</td><td>In CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</td></tr>
<tr>
<td>ID of the referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul></td><td><ul  style="margin: 0;"><li>To reference the current security group, enter the ID of security group associated with the CVM.</li><li>You can also reference another security group in the same region and the same project by entering the security group ID.</li></ul></td></tr>
<tr>
<td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
   - **Protocol Port**: enter the protocol type and port range or reference a protocol/port or protocol/port group in a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).
>?To connect to TencentDB for MongoDB, port 27017 must be opened. 
   - **Policy**: **Allow** or **Reject**. **Allow** is selected by default.
     - **Allow**: traffic to this port is allowed.
     - **Reject**: data packets will be discarded without any response.
   - **Remarks**: a short description of the rule for easier management.
5. Click **Complete**.
   
### Step 3. Bind the security group to an instance
>!Currently, security groups can be configured only for TencentDB for MongoDB instances in VPC.

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **More** > **Security Group**.
You can also click the target instance name, select the **Security Group** tab, and click **Configure Security Group**.
6. In the **Configure Security Group** pop-up window, select the target security group and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/6e9a53e1c4131f4c73a84af2213cfde9.png)

## More Operations
### Adjusting the priority of bound security group
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID, select the **Security Group** tab, and view all security groups of the instance.
6. Click **Edit**. You can click <img src="https://qcloudimg.tencent-cloud.cn/raw/b407f850a15a1362a1ac89a4b13ce955.png" style="zoom: 80%;" /> or <img src="https://qcloudimg.tencent-cloud.cn/raw/3efb762c31ec14fa16813748183eb520.png" style="zoom:80%;" /> in the **Operation** column to adjust the filtering priorities of security groups.
7. Click **Save**.

### Adjusting inbound/outbound rule
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. Click the target instance ID, select the **Security Group** tab, and view all security groups of the instance.
6. In the security group list, click the target **security group ID** or name to enter the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page.
7. Find the security group rule to be modified and click **Edit** in the **Operation** column to edit it.

### Importing security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click the ID/name of a security group.
2. On the **Inbound Rule** or **Outbound Rule** tab, click **Import Rule**.
3. In the pop-up window, select an edited inbound/outbound rule template file and click **Import**.
>? 
>- As existing rules will be overwritten after importing, we recommend you export the existing rules before importing new ones.
>- If there are no existing rules in the security group, download a template and edit it before importing it.

### Cloning security group
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the target security group and click **More** > **Clone** in the **Operation** column.
2. In the pop-up window, select the target region and project and click **OK**.
If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

### Deleting security group
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the security group to be deleted and click **More** > **Delete** in the **Operation** column.
2. In the pop-up window, click **OK**.
If the current security group is associated with a CVM instance, it must be disassociated first before it can be deleted.

## References
For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/213/12452).

