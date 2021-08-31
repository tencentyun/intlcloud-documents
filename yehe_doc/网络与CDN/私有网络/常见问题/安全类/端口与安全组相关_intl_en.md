## Port-Related Questions
### Why does a port have to be enabled, and how can I enable a specific port?
You can use the services corresponding to a port only after opening the port in the security group. For example:
To access web pages through port 8080, this port must be enabled and opened to Internet in the security group.
Step-by-step instructions for opening a certain port to the Internet are as follows:
1. Log in to [Security Group Console](https://console.cloud.tencent.com/vpc/securitygroup) and click the security group that is bound with this instance to go to the details page.
2. Choose **Inbound/Outbound Rules** and click **Add Rule**.
3. Enter your IP address (or IP range) and the port to be opened, and then select **Allow** to open the port.

### Why is the service unavailable after the port has been modified?
After modifying the service port, you must additionally open the port in the corresponding security group before the service can be used.

### Which ports are not supported by Tencent Cloud?
The following ports are blocked by the carrier due to security considerations. We recommend that you use other ports than the following for listening:

| Protocol | Unsupported Ports |
| ---- | ---------------------------------------- |
| TCP | Ports 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, and 9996 |
| UDP | Ports 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, and 135-139 |

### Why cannot TCP port 25 be used to connect to an external address, and how can I unblock the port?
- To enhance the quality of sending emails through Tencent Cloud’s IP addresses, CVMs are blocked by default from using TCP port 25 to connect to external addresses. To unblock this port, you can log in to the [console](https://console.cloud.tencent.com/), hover over the account navigation area at the top, and click **Security Control** to view the link for unblocking port 25.
- By default, each user can unblock up to five instances in each region.

For more port-related instructions, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/215/35520).

## Security Group-Related Questions
### Why is a rejection rule set in a security group by default?
Security group rules take effect in order from top to bottom. Therefore, after the allowance rule that was set first is validated, other rules will be invalidated by default. If the rule opens all ports to the Internet, the last rejection rule will be invalid. This default setting is provided for security concerns.

### If I bind an instance with the incorrect security group, what will be the impact on the instance, and how can I fix this?
- **Potential problems**
 - You may fail to remotely connect to a Linux instance (through SSH) or remotely log in to a Windows desktop instance.
 - You may fail to remotely ping the public or private IP address of a CVM instance in this security group.
 - You may fail to gain HTTP access to the web services opened by a CVM instance in this security group.
 - You may fail to access the Internet through an instance in this security group.
- **Solutions**
 - In case any of the preceding problems occurs, you can go to "Security Group Management" in the console and edit the rule for the security group, for example, to "only bind all-pass security groups by default".
 - For details on setting security group rules, see [Security Groups - Security Group Rules](http://intl.cloud.tencent.com/document/product/213/12452).

### What do a security group direction and a policy mean?
- Security group policies work in the directions of outbound and inbound. The outbound direction is to filter the outbound traffic of the CVM, whereas the inbound direction is to filter the inbound traffic of the CVM.
- Security group policies are divided into policies that **allow** or **reject** traffic.

### What is the order in which security group policies take effect?
The order in which security group policies take effect is from top to bottom. Traffic goes through the security group’s policy matching in order from top to bottom, and the first hit policy will take effect.

### Why can an IP address that is rejected by the security group access the CVM?
The possible reasons for this issue are:
- The CVM may be bound to multiple security groups, and the IP address is allowed by another security group.
- The IP address belongs to an approved Tencent Cloud public service.

### Does using security groups mean that iptables cannot be used?
No, security groups and iptables can be used simultaneously. In this case, your traffic will be filtered twice in the following directions:
- Outbound: processes in your instance > iptables > security groups.
- Inbound: security groups > iptables > processes in your instance.

### Why cannot security groups be deleted even after all CVMs have been returned?
Check Recycle Bin for any CVMs. The deletion will fail if security groups are bound to CVMs in Recycle Bin.

### Is there any cloud API that supports cloning a security group across different projects and regions?
Console support is available to customers who are using the console, but no cloud API support is available for now. You can use the original cloud APIs for importing or exporting security group rules in batches to indirectly clone a security group across different projects and regions.

### When I clone security groups across projects and regions, will CVMs managed by the security groups also be copied?
No, cloning a security group across different regions clones only the inbound and outbound rules of the original security group. In this case, CVMs must be associated separately.
