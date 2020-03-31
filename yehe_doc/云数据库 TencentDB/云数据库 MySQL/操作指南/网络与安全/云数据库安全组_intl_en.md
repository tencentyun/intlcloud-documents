## Operation Scenarios
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list and are matched with each other within the security group based on rules. 

>
>- TencentDB for MySQL security group currently only supports network access control for VPCs and public network but not the basic network.
>- Security groups that currently support public network access are available only in the Guangzhou, Shanghai, Hong Kong (China), Beijing, Chengdu, Chongqing, Seoul, and Tokyo regions.
>- As no outbound traffic is generated for TencentDB instances, outbound rules do not take effect for TencentDB.
>- TencentDB for MySQL security groups support master instances, read-only instances, and disaster recovery instances.
>- Security group is not supported for the TencentDB for MySQL Basic Edition.


## Directions
### Step 1. Create a security group
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region, and click **Create**.
3. In the pop-up dialog box, configure the following items and click **OK**.
 - Template: select an appropriate template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
	<tr><th>Template</th><th>Description</th><th>Scenario</th></tr>
	<tr><td>Open all ports</td><td>All ports are opened to the internet. This may present security issues.</td><td>-</td></tr>
	<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This is suitable for security groups containing instances with web services deployed.</td></tr>
	<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, please see <a href="https://intl.cloud.tencent.com/document/product/236/14470">Adding Security Group Rules</a>.</td><td>-</rd></tr>
</table>
 - Name: custom name of the security group.
 - Project: the **default project** is selected by default. You can also select another one for easier management.
 - Remarks: a short description of the security group.


 <span id="Step2"></span>
### Step 2. Add a security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click **Modify Rules** in the "Operation" column on the row of the security group for which to configure a rule.
2. <span id="step02">On the security group rule page, click **Inbound Rules** and choose one of the following methods to add a rule.</span>
> Method 2 "Add a rule" is used below as an example.
>
 - Method 1. Open all ports: this method is ideal if you do not need custom ICMP rules and all traffic goes through ports 22, 3389, 80, 443, 20, and 21 and the ICMP and ICMPv6 protocols.
 - Method 2. Add a rule: this method is ideal if you need to use multiple protocols such as ICMP.
3. In the pop-up dialog box, set the rule.
 - Type: "Custom" is selected by default. You can also choose another system rule template, such as MySQL (3306).
 - Source: traffic source (inbound rule) or destination (outbound rule). You need to specify one of the following options:
<table>
	<tr><th>Source/Destination</th><th>Description</th></tr>
	<tr><td>IPv4 address or IPv4 address range</td><td>In CIDR format (such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses).</td></tr>
	<tr><td>IPv6 address or IPv6 address range</td><td>In CIDR format (such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicate all IPv6 addresses).</td></tr>
	<tr><td>ID of referenced security group. You can reference the ID of: <ul  style="margin: 0;"><li>Current security group</li><li>Another security group</li></ul>
</td><td><ul  style="margin: 0;"><li>Current security group: CVM instance associated with the current security group.</li><li>Another security group: ID of another security group in the same region under the same project.</li></ul>
</td></tr>
	<tr><td>Referenced IP address object or IP address group object in a parameter template.</td><td>-</td></tr>
</table>
 - Protocol port: enter the protocol type and port range or reference an IP address object or IP address group object in a parameter template.
 - Policy: "Allow" is selected by default.
    - Allow: access requests to this port are allowed
    - Reject: data packets will be discarded without any response.
 - Remarks: a short description of the rule for easier management.
4. <span id="step04">Click **Complete** to finish adding the inbound rule.</span>
5. On the security group rule page, click **Outbound Rules** to add an outbound rule as instructed in [step 2](#step02) to [step 4](#step04).


### Step 3. Configure a security group for TencentDB
A security group is an instance-level firewall provided by Tencent Cloud for controlling inbound/outbound traffic of TencentDB. You can associate a security group with an instance when purchasing it or later in the console.

>Currently, security groups can be configured only for **TencentDB for MySQL instances in VPC**.

1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb).
2. In the instance list, select the instance for which to configure a security group and click **Manage** in the "Operation" column to enter the instance management page.
3. On the **Security Group** tab, click **Configure Security Group**.
4. In the pop-up dialog box, select the security group to be bound and click **OK**. 

## Cloning a Security Group
1. On the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select a security group and click **More** > **Clone** in the "Operation" column.
2. In the pop-up dialog box, select the target region and target project and click **OK**. If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

## Importing/Exporting a Security Group Rule
1. On the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select the security group to be updated and click its ID/name to enter its details page where you can find tabs for inbound rules and outbound rules.
2. On the "Inbound Rules" or "Outbound Rules" tab, click **Import Rules**.
3. If you already have a rule, you are recommended to export it first, as importing a rule will overwrite the existing one. If no rule exists, export a template first, edit the template file, click **Select File** in the pop-up dialog box to select the edited file, and click **Start Import**.	

## Deleting a Security Group
1. On the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select the security group to be deleted and click **More** > **Delete** in the "Operation" column.
2. Click **OK** in the pop-up dialog box. If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.


