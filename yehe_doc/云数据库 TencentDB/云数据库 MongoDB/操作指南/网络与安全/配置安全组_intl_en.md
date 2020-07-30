## Operation Scenarios
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is a stateful virtual firewall capable of filtering. As an important means for network security isolation provided by Tencent Cloud, it can be used to set network access controls for one or more TencentDB instances. Instances with the same network security isolation demands in one region can be put into the same security group, which is a logical group. TencentDB and CVM share the security group list.

>
> - TencentDB security group currently only supports network access control for VPC private network but not the basic network.
>- As no outbound traffic is generated for TencentDB instances, outbound rules do not take effect for TencentDB.
> - TencentDB for MongoDB security groups support master instances, read-only instances, and disaster recovery instances.
>- TencentDB for MongoDB (expect for 4.0 replica sets) supports the security group feature which is implemented based on the allowlist. To use this feature, please [submit a ticket]

## Configuring Security Group for TencentDB
### Step 1. Create a security group
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/securitygroup).
2. Select **Security Group** on the left sidebar, select a region, and click **Create**.
3. In the pop-up dialog box, configure the following items and click **OK**.
 - Template: select an appropriate template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
<tr><th>Template</th><th>Description</th><th>Remarks</th></tr>
<tr><td>Open all ports</td><td>All ports are opened to the public and private networks. This may present security issues.</td><td>-</td></tr>
<tr><td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This template does not take effect for TencentDB.</td></tr>
<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, please see "Adding Security Group Rules"</a> below.</td><td>-</rd></tr>
</table>
 - Name: custom name of the security group.
 - Project: the **default project** is selected by default. You can also select another one for easier management.
 - Remarks: a short description of the security group for easier management.


 <span id="Step2"></span>
### Step 2. Add a security group rule
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click **Modify Rule** in the "Operation" column on the row of the security group for which to configure a rule.
2. <span id="step02">On the security group rule page, click **Inbound Rules** > **Add Rule**.</span>
3. In the pop-up dialog box, set the rule.
 - Type: "Custom" is selected by default. You can also choose another system rule template.
 - Source: traffic source (inbound rule) or destination (outbound rule). You need to specify one of the following options:
<table>
<tr><th>Source/Destination</th><th>Description</th></tr>
<tr><td>IPv4 address or IPv4 address range</td><td>In CIDR format (such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses).</td></tr>
<tr><td>IPv6 address or IPv6 address range</td><td>In CIDR format (such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicate all IPv6 addresses).</td></tr>
<tr><td>ID of referenced security group. You can reference the ID of: <ul  style="margin: 0;"><li>Current security group</li><li>Another security group</li></ul>
</td><td><ul  style="margin: 0;"><li>Current security group: CVM instance associated with the current security group.</li><li>Another security group: ID of another security group in the same region under the same project.</li></ul>
</td></tr>
<tr><td>Reference IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - Protocol port: enter the protocol type and port range or reference an IP address object or IP address group object in a [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).
  >To connect to TencentDB for MongoDB, port 27017 must be opened.
 - Policy: "Allow" is selected by default.
    - Allow: traffic to this port is allowed.
    - Reject: data packets will be discarded without any response.
 - Remarks: a short description of the rule for easier management.
4. <span id="step04">Click **Complete** to finish adding the inbound rule.</span>

          
### Step 3. Configure a security group
A [security group](https://intl.cloud.tencent.com/document/product/213/12452) is an instance-level firewall provided by Tencent Cloud for controlling inbound/outbound traffic of TencentDB. You can associate a security group with an instance when purchasing it or later in the console.

> Currently, security groups can be configured only for TencentDB for MongoDB instances in VPC.

1. Log in to the [TencentDB for MongoDB Console](https://console.cloud.tencent.com/mongodb), select **More** > **Security Group** in the **Operation** column in the instance list.
2. Select the security group to be bound and click **Confirm** to bind the security group to TencentDB for MongoDB.

## Importing Security Group Rules
1. On the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, click the ID/name of the desired security group.
2. On the inbound rules or outbound rules tab, click **Import Rule**.
7. In the pop-up dialog box, select an edited inbound/outbound rule template file and click **Start Import**.
>
>- If there are existing rules in the security group, export them before importing new rules. Existing rules are overwritten after importing.
>- If there are no existing rules in the security group, download a template and edit it before importing it.
>

## Cloning Security Group
1. On the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select a security group and click **More** > **Clone** in the "Operation" column.
2. In the pop-up dialog box, select the target region and target project and click **OK**. If the new security group needs to be associated with a CVM instance, do so by managing the CVM instances in the security group.

## Deleting Security Group
1. On the [security group page](https://console.cloud.tencent.com/cvm/securitygroup), select the security group to be deleted and click **More** > **Delete** in the "Operation" column.
2. Click **OK** in the pop-up dialog box. If the current security group is associated with a CVM instance, it must be disassociated before it can be deleted.
