Security groups are used to manage traffic to and from public and private networks. For the sake of security, most inbound traffic is denied by default, but you can modify and add security group rules as needed. This document describes how to modify and add security group rules in the console.

## Prerequisites
- You have created a security group. For more information, see [Configuring Security Group] (https://www.tencentcloud.com/document/product/1098/44594) .
- You have learned about which traffic is allowed or denied for your CVM instance. For more information on security group rules and their use cases, see [Security Group Use Cases] (https://intl.cloud.tencent.com/document/product/213/32369).

## Modifying Security Group Rules
1. Log in to the CVM console and go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the created target security group, and click **Modify Rule** in the **Operation** column.
2. On the security group rule page, select inbound or outbound rules by clicking **Inbound rules** or **Outbound rules**.
3. Locate the desired rule and click **Edit** to modify it.

## Adding Security Group Rules
1. Log in to the CVM console and go to the [Security Group](https://console.cloud.tencent.com/cvm/securitygroup) page, find the created target security group, and click **Modify Rule** in the **Operation** column.
2. On the security group rule page, click **Inbound Rules** > **Add Rule**.
3. In the pop-up dialog box, set the rule.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9MhQ015_1.png)
 - **Type**: **Custom** is selected by default. You can also choose another system rule template. MySQL(3306) is recommended.
 - **Source** or **Destination**: traffic source (inbound rules) or target (outbound rules). You need to specify one of the following options:
<table>
	<tr><th>Source or Target</th><th>Description</th></tr>
	<tr><td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
	<tr><td>A single IPv6 address or an IPv6 range</td><td>In CIDR notation, such as <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses will be matched.</td></tr>
	<tr><td>ID of referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul>
</td><td><ul  style="margin: 0;"><li>To reference the current security group, please enter the ID of security group associated with the CVM.</li><li>You can also reference another security group in the same region and the same project by entering the security group ID.</li></ul>
</td></tr>
	<tr><td>Reference an IP address object or IP address group object in a <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - **Protocol Port**: Enter the protocol type and port range or reference a protocol/port or protocol/port group in a [parameter template management](https://intl.cloud.tencent.com/document/product/215/31867).
>!
>- To connect to TDSQL-C for MySQL, you need to open its instance port. You can log in to the [TDSQL-C for MySQL console] (https://console.cloud.tencent.com/cynosdb), click the cluster ID to enter the details page, and view its port in the **Connection Info** section.
>- The security group rules displayed on the **Security Group** page in the TDSQL-C MySQL console take effect for private and public (if enabled) network addresses of the TencentDB for MySQL instance.
>
 - **Policy**: **Allow** or **Reject**. **Allow** is selected by default.
    - **Allow**: Traffic to this port is allowed.
    - **Reject**: Data packets will be discarded without any response.
 - **Notes**: A short description of the rule for easier management.
4. Click **Complete**
5. On the security group rule page, click **Outbound rule** and refer to Steps 2-4 for adding an outbound rule.
