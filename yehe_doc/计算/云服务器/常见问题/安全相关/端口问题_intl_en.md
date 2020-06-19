This document describes FAQs pertaining to security groups and port configuration.
- For more information on how to create, configure, and manage a security group in the console, see the following documents:
 - [Creating a Security Group](https://intl.cloud.tencent.com/document/product/213/34271)
 - [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/213/34272)
 - [Managing Security Groups](https://intl.cloud.tencent.com/document/product/213/34828)
 - [Managing Security Group Rules](https://intl.cloud.tencent.com/document/product/213/34826)
- If you are proficient in using Cloud Virtual Machine (CVM) APIs, you can also use [security group APIs](https://intl.cloud.tencent.com/document/product/213/12447) to configure and manage security groups.

## Port-Related FAQs

### Which port(s) should be opened to the Internet before I log in to an instance?
Generally, you need to open port 22 for Linux instances, or port 3389 for Windows instances. For more information on ports that need to be opened for other types of instances, see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/213/32369).

### Which ports are commonly used in CVM?

For more information, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451).

### Why should a port be opened to the Internet, and how can I open a specific port to the Internet?

You can use the services corresponding to a port only after opening the port to the Internet in the security group. For example:
To access web pages through port 8080, the port must be opened to the Internet in the security group.
Directions for opening a port to the Internet are as follows:
1. Log in to the [Security Group Console](https://console.cloud.tencent.com/vpc/securitygroup) and click the security group bound to this instance to go to the details page.
2. Select **Inbound/Outbound Rules** and click **Add Rule**.
3. Enter the IP address (range) and port to be opened, and then select **Allow** to open the port to the Internet.
For more information on directions, see [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/213/34272).

### How can I change the default remote port of a CVM instance?

For more information, see [Changing the Default Remote Port of a CVM Instance](https://intl.cloud.tencent.com/document/product/213/35376).


### Why can I not use the service after modifying the port?

After changing the service port, you also need to open the port to the Internet in the corresponding security group before you can use the service.

### Which ports are not supported by Tencent Cloud?

- By default, TCP port 25 is blocked by Tencent Cloud. To unblock this port, see [Unblocking Port 25](https://intl.cloud.tencent.com/document/product/213/34833).
- Some ports can incur security risks. Although these ports are not blocked by Tencent Cloud, they are still blocked by ISPs and therefore inaccessible. To prevent this problem, we recommend that you change ports and do not use the following ports for listening:
<table>
<tr><th>Protocol</th><th>Ports That May Be Blocked</th></tr>
<tr><td>TCP</td><td>Ports 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, and 9996</td></tr>
<tr><td>UDP</td><td>Ports 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, and 135-139</td></tr>
</table>
