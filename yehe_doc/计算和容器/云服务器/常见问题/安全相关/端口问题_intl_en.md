### Which ports should be opened to the Internet before I log in to an instance?
Generally, you need to open port 22 for a Linux instance, or port 3389 for a Windows instance. For more information about ports applicable to other instance types, see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).

### Which ports are often used in CVM?

For more information, see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).

### Why should a port be opened to the Internet? How can I open a specific port?

You can use the service only after you open the port to the Internet in the security group. For example:
If you want to access web pages using port 8080, the port must be enabled and opened to the Internet in the security group.
To open a port to the Internet, follow the steps below:
1. Go to the [security group page](https://console.cloud.tencent.com/vpc/securitygroup), and click the ID/name of the security group bound with this instance to go to its details page.
2. Select **Inbound/Outbound rule** and click **Add a Rule**.
3. Enter your IP address (range) and port to be opened, and then select **Allow** to open the port.
For more information, see [Adding Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34272).

### How can I change the default remote port of a CVM instance?

For more information, see [Modifying the Default Remote Port of CVM](https://intl.cloud.tencent.com/document/product/213/35376).


### Why cannot the service be used after I change the port?

After modifying the service port, you also need to open the corresponding port to the Internet in the security group.

### Which ports are not supported by Tencent Cloud?

- By default, TCP port 25 is blocked by Tencent Cloud. If you need to unblock this port, see [Unblocking Port 25](https://intl.cloud.tencent.com/document/product/213/34833).
- Some ports have security risks. Although these ports are not blocked by Tencent Cloud, they will be blocked by ISPs and cannot be accessed. To avoid this, we recommend that you change ports and do not use the following ports for listening:
<table>
<tr><th>Protocol</th><th>Blocked Port</th></tr>
<tr><td>TCP</td><td>42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, 9996</td></tr>
<tr><td>UDP</td><td>1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, 135 - 139</td></tr>
</table>


### Why cannot I use TCP 25 port?
TCP port 25 is the default email service port. For security reasons, port 25 of CVM instances is blocked by default. If you need to use it, see [Unblocking Port 25](https://intl.cloud.tencent.com/document/product/213/34833).

