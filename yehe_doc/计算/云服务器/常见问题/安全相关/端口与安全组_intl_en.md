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


## Security Group-Related FAQs

### Why does a security group have a reject rule by default?

Security group rules take effect sequentially from top to bottom. If an allow rule that is previously set takes effect, later rules are rejected by default. If this allow rule opens all ports to the Internet, the last reject rule does not take effect. We provide this default setting due to security concerns.

### How can I adjust the priority of a security group?

For more information, see [Adjusting the Priority of a Security Group](https://intl.cloud.tencent.com/document/product/213/35375).

### If I bind an incorrect security group to an instance, what is the impact on the instance, and how can I correct this problem?

**Potential problems**

- You may fail to remotely connect to a Linux instance (over SSH) or remotely log in to a desktop Windows instance.
- You may fail to remotely ping the public and private IP addresses of the CVM instance in this security group.
- You may fail to access the web services exposed by the CVM instance in this security group over HTTP.
- The CVM instance in this security group may fail to access Internet services.

**Solutions**

- If any of the preceding problems happens, you can go to "Security Group Management" in the console and change the security group rule. For example, you can change the rule to "bind only all-ports-open security groups by default".
- For more information on how to define a security group rule, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

### What are the direction and policy of a security group?

Security group policies are divided into outbound and inbound. Outbound filters the outbound traffic of the CVM instance, whereas inbound filters the inbound traffic of the CVM instance.
Security group policies are divided into those that **Allow** and **Reject** traffic.

### In which order do security group policies take effect?

Security group policies take effect sequentially from top to bottom when traffic flows through the security group. When the traffic matches a policy, the policy takes effect immediately.

### Why can an IP address that is rejected by a security group still access the CVM instance?

Possible reasons are as follows:
- The CVM is bound to multiple security groups, and this IP address is allowed by another security group among them.
- This IP address belongs to an approved Tencent Cloud public service.

### Can iptables be used along with security groups?

Yes. Security groups and iptables can be used at the same time. Your traffic will be filtered twice in the following directions:
- Outbound: processes in your instance > iptables > security groups.
- Inbound: security groups > iptables > processes in your instance.

### Why can security groups not be deleted when all CVM instances have been returned?

Check whether any CVM instances still exist in the recycle bin. If security groups are still bound to a CVM instance in the recycle bin, they cannot be deleted.

### Can the name of a cloned security group be the same as that of a security group in the target region?

No. The name must be different from that of any existing security group in the target region.

### Can a security group be cloned across different users?

No. This feature is currently not supported.

### Is there any Tencent Cloud API that supports the cloning of a security group across projects and regions?

MC support is provided to help customers who use the console, but no Tencent Cloud API can be directly used for this purpose at the moment. You can use original Tencent Cloud APIs for batch import and export of security group rules to indirectly clone a security group across projects and regions.

### When I clone a security group across projects and regions, will CVM instances managed by the security group also be copied?

No. When a security group is cloned across regions, only the inbound and outbound rules of the original security group are copied. Therefore, you need to bind CVM instances to the security group separately.
