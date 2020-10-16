## Port
### Which ports should be opened to the Internet before I log in to an instance?
Generally, you need to open port 22 for a Linux instance, or port 3389 for a Windows instance. For more information about ports applicable to other instance types, see [Application Cases of Security Groups](https://intl.cloud.tencent.com/document/product/215/35519).

### Why should a port be opened to the Internet? How can I open a specific port?
You can use the service only after you open the port to the Internet in the security group. For example:
If you want to access web pages using port 8080, the port must be enabled and opened to the Internet in the security group.
To open a port to the Internet, follow the steps below:
1. Go to the [security group](https://console.cloud.tencent.com/vpc/securitygroup) page, and click the ID/name of the security group bound with this instance to go to its details page.
2. Select **Inbound/Outbound rule** and click **Add a Rule**.
3. Enter your IP address (range) and port to be opened, and then select **Allow** to open the port.
For more information, see [Adding a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35513).

### Why cannot the service be used after I change the port?
After modifying the service port, you also need to open the corresponding port to the Internet in the security group.

### Which ports are not supported by Tencent Cloud?
The following ports have security risks. They will be blocked by ISPs and cannot be accessed. To avoid this, we recommend that you change ports and do not use the following ports for listening:

| Protocol   | Blocked Port                           |
| ---- | ---------------------------------------- |
| TCP  | 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900 and 9996 |
| UDP  | 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433 and 135 - 139 |

## Why cannot TCP port 25 be used to connect to an external address, and how can I unblock the port?
- To enhance the quality of sending emails through Tencent Cloud’s IP addresses, CVMs are blocked by default from using TCP port 25 to connect to external addresses. To unblock this port, you can log in to the [console](https://console.cloud.tencent.com/), hover over the account navigation area at the top, and click **Security Control** to view the link for unblocking port 25.
- You can only unblock the port on a maximum of five monthly subscription CVM instances. However, pay-as-you-go CVM are not supported yet.

For more information about ports, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/215/35520).

## Security Group
### Why does a security group have a reject rule by default?
Security group rules take effect sequentially from top to bottom. If an allow rule that was previously set takes effect, other rules will be rejected by default. If this allow rule opens all ports to Internet, the last reject rule will not take effect. We provide this default setting due to security concerns.

### If I bind an incorrect security group to an instance, what impact will this have on the instance? How can I fix this problem?
- **Potential problems**
 - You may fail to remotely connect to a Linux instance over SSH or a Windows instance via remote desktop.
 - You may fail to remotely ping the public IP and private IP addresses of the CVM instance in this security group.
 - You may fail to access over HTTP the web services exposed by the CVM instance in this security group.
 - The CVM instance in this security group may fail to access Internet services.
- **Solutions**
 - If any of the aforementioned problems occur, you can go to **Security Groups** on the console and modify the security group rule. For example, you can change the rule to "bind only all-ports-open security groups by default".
 - For more information on how to set a security group rule, see “Security Group Rules” section of [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452#.E5.AE.89.E5.85.A8.E7.BB.84.E8.A7.84.E5.88.99).

### What do the security group direction and policy mean?
- There are outbound and inbound security group directions. The outbound direction filters the outbound traffic of the CVM instance, whereas the inbound direction filters the inbound traffic of the CVM instance.
- Security group policies are divided into those that **allow** or **reject** traffic.

### In which order do the security group policies take effect?
Security group policies take effect sequentially from top to bottom when traffic flows through the security group. Once the traffic matches a policy, the policy will take effect immediately.

### Why can’t a port that is opened to the Internet by a security group access the CVM instance?
- The CVM is bound to multiple security groups, and this port is rejected by another security group with a higher priority.
- The network ACL or firewall has been configured.

### Why can an IP address that is rejected by a security group still access the CVM instance?
Possible reasons are as follows:
- The CVM is bound to multiple security groups, and this IP address is allowed by another security group among them.
- This IP address belongs to an approved Tencent Cloud public service.

### Can iptables be used along with security groups?
Yes. Security groups and iptables can be used at the same time. Your traffic will be filtered twice in the following directions:
- Outbound: processes in your instance > iptables > security groups.
- Inbound: security groups > iptables > processes in your instance.

### Why can’t security groups be deleted even though all CVM instances have been returned?
Check whether any CVM instances still exist in the recycle bin. If security groups are still bound to a CVM instance in the recycle bin, they cannot be deleted.

### Can the name of a cloned security group be the same as that of a security group in the target region?
No. The name must be different from that of any existing security group in the target region.

### Is there any Tencent Cloud API that supports the cloning of a security group across projects and regions?
While console support is provided to help customers who use the console, no Tencent Cloud API can be directly used for this purpose at the moment. You can use the original Tencent Cloud APIs for batch importing and exporting of security group rules to indirectly clone a security group across projects and regions.

### When I clone a security group across projects and regions, will CVM instances managed by the security group also be copied?
No. When a security group is cloned across regions, only the inbound and outbound rules of the original security group will be copied. Therefore, you need to bind CVM instances to the security group separately.
