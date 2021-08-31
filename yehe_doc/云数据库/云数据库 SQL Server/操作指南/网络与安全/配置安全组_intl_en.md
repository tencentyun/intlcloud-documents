## Overview
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. For specific rules and use limits, see [Security Group Overview](https://intl.cloud.tencent.com/document/product/215/38750).

>?
>- TencentDB for SQL Server security group currently only supports network access control for VPCs and public network but not the classic network.
>- Security groups that currently support public network access are available only in Guangzhou, Shanghai, Beijing, and Chengdu.
>- As TencentDB does not have active outbound traffic, outbound rules are not applicable to TencentDB.
>- TencentDB for SQL Server security group supports primary instances and read-only replicas.


## Security Group Configuration for TencentDB
### Step 1. Create a security group
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region, and click **+New**.
3. In the pop-up dialog box, configure the following items and click **OK**.
 - **Template**: select a template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
	<tr><th>Template</th><th>Description</th><th>Remarks</th></tr>
	<tr><td>Open all ports</td><td>All ports are open. May present security issues.</td><td>-</td></tr>
	<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This template does not take effect for TencentDB.</td></tr>
	<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, please see "Step 2. Add a security group rule"</a> below.</td><td>-</rd></tr>
</table>
 - **Name**: name of the security group.
 - **Project**: by default, **DEFAULT PROJECT** is selected. Select a project for easier management.
 - **Notes**: a short description of the security group for easier management.



### Step 2. Add a security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click **Modify Rules** in the **Operation** column on the row of the security group for which to configure a rule.
2. Select **Security Group Rule** > **Inbound rule**, click **Add a Rule**.
3. In the pop-up dialog box, set the rule.
 - **Type**: **Custom** is selected by default. You can also choose another system rule template. SQL Server(1433) is recommended.
 - **Source** or **Target**: traffic source (inbound rules) or target (outbound rules). You need to specify one of the following options:
<table>
	<tr><th>Source or Destination</th><th>Description</th></tr>
	<tr><td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
	<tr><td>A single IPv6 address or an IPv6 range</td><td>In CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</td></tr>
	<tr><td>ID of referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul>
</td><td><ul  style="margin: 0;"><li>Current security group: CVMs associated with the current security group.</li><li>Other security group: ID of another security group in the same region that belongs to the same project.</li></ul>
</td></tr>
	<tr><td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - **Protocol port**: enter the protocol type and port range or reference a protocol/port or protocol/port group in a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).
  >?To connect to TencentDB for SQL Server, port 1433 must be opened.
 - **Policy**: **Allow** or **Refuse**. **Allow** is selected by default.
    - **Allow**: traffic to this port is allowed.
    - **Refuse**: data packets will be discarded without any response.
 - **Notes**: a short description of the rule for easier management.
4. Click **Complete**.

#### Use cases
**Scenario:** you have created a TencentDB for SQL Server instance and want to access it from a CVM instance.
**Solution:** when adding security group rules, select **SQL Server(1433)** in **Type** to open port 1433.
You can also allow all IPs or specified IPs (IP ranges) based on your actual needs so as to configure IP sources that can access TencentDB for SQL Server through CVM.

| Direction | Type | Source | Protocol and Port | Policy |
|---------|---------|---------|---------|---------|
| Inbound | SQL Server(1433) | All IP: 0.0.0.0/0 <br>Specified IP: enter the specified IPs or IP ranges | TCP:1433 | Allow |


### Step 3. Configure a security group
A security group is an instance-level firewall provided by Tencent Cloud for controlling inbound traffic to TencentDB. You can associate a security group with an instance when purchasing it or later in the console.

>!Currently, only **TencentDB for SQL Server in VPC** can associate with security groups.

1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver). In the instance list, locate the instance for which to configure a security group and click **Manage** in the **Operation** column to enter the instance management page.
2. On the **Security Group** page, click **Configure Security Group**.
3. In the pop-up dialog box, select the security group to be associated and click **OK**. 

## Security Group Rule Import
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click the ID/name of the target security group.
2. On the **Inbound rule** or **Outbound rule** tab, click **Import rule**.
3. In the pop-up dialog box, select an edited inbound/outbound rule template file and click **Import**.
>? If there are existing rules in the security group, export them before importing new rules. Existing rules are overwritten after importing.


## Security Group Clone
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, locate the desired security group and click **More** > **Clone** in the **Operation** column.
2. In the pop-up dialog box, select the region and project, enter a new name for the security group, and click **OK**. If the new security group needs to be associated with a CVM instance, click **Manage Instances** in the **Operation** column to add a CVM instance on the **Associate with Instance** > **Cloud Virtual Machine** tab.

## Security Group Deletion
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, locate the security group to be deleted and click **More** > **Delete** in the **Operation** column.
2. Click **OK** in the pop-up dialog box. If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.

