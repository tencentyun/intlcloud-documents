## Port-related FAQs
### Which ports should I open before logging in to an instance?
Generally, you need to open port 22 for a Linux instance, or port 3389 for a Windows instance. For more information, see [Application Cases of Security Groups](https://www.tencentcloud.com/document/product/215/35519).

### Why should I open a port, and how?
You should open the port in the security group to use related services. 
For example, if you want to access web pages using port 8080, you should open this port in the security group.
Steps to open a port: 
1. Log in to the [security group console](https://console.cloud.tencent.com/vpc/securitygroup), and click the ID/name of the security group bound with this instance to enter its details page.
2. Select **Inbound/Outbound rule** and click **Add a Rule**.
3. Enter your IP address (range) and port to be opened, and then select **Allow**.
For details of directions, see [Adding a Security Group Rule](https://www.tencentcloud.com/document/product/215/35513).

### My business is not accessible after I modified the port.
After modifying the service port, you need to open the corresponding port in the security group.

### Which ports are not supported by Tencent Cloud?
The following ports are not allowed as they have security risks and are very likely to be blocked by ISPs.

| Protocol   | Unsupported ports                            |
| ---- | ---------------------------------------- |
| TCP  | 42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900 and 9996 |
| UDP  | 1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433 and 135 - 139 |

## I cannot connect to an external address through TCP port 25.
- To enhance the quality of sending emails through Tencent Cloud’s IP addresses, CVMs are blocked from using TCP port 25 to connect to external addresses by default. To unblock this port, you can log in to the [console](https://console.cloud.tencent.com/), hover over the account navigation area at the top, and click **Security Control** to view the link for unblocking port 25.
- Each account supports unblocking the CVMs 5 times. Note that pay-as-you-go CVMs are not supported.

For more information about ports, see [Common Server Ports](https://www.tencentcloud.com/document/product/215/35520).

## Security Group-related FAQs

### What if an improper security group is selected? How can this be fixed?
- **Risks**
 - Fail to remotely connect to a Linux instance (SSH) or remotely log in to desktop Windows instance.
 - Fail to ping the public/private IP of the CVMs in this security group.
 - Fail to access over HTTP the web services exposed by the CVM instance in this security group.
 - You may fail to access the Internet with the instance under this security group.
- **Solutions**
 - In case any of the above problems happens, you can go to "Security Group Management" in the console and reset the rule for the security group, for example, to "only bind all-pass security groups by default".
 - For details of setting security group rules, see [Security Group - Security Group Rules](https://www.tencentcloud.com/document/product/213/12452).

### What do security group direction and policy mean?
- The security group policy works in the directions of outbound and inbound. The former is to filter the outbound traffic of the CVM, and the latter is to filter the inbound traffic of the CVM.
- Security group policies include **Allow** and **Refuse**.

### What is the order in which security group policies to go into effect?
The order that security group policies go into effect is from top to bottom. Traffic passes through the security group’s matching sequence from top to bottom, and the policy goes into effect as soon as there is a successful match.

### I opened a port in the security group, but the CVM is still not accessible. 
- Check whether the CVM is bound to with another higher-priority security group, which reject this port.
- The port is blocked by the network ACL or firewall.
- The service corresponding to the port is not started.
- The port is not open in the system firewall.

### How come an IP that is not allowed in the security group can still access the CVM?
Possible reasons: 
- The CVM is bound to multiple security groups, and the IP is allowed by another security group.
- This IP address belongs to an approved Tencent Cloud public service.

### Can iptables be used along with security groups?
Yes. Security groups and iptables can be used at the same time. Your traffic will be filtered twice in the following directions:
- Outbound: Processes in your instance > iptables > security groups.
- Inbound: Security groups > iptables > processes in your instance.

### I have returned all CVMs associated with the security group. But I still cannot delete the security group.
Besides CVMs, a security group can also be bound with CLB, ENI and cloud database instances. Please make sure that all resources bound with the security group have been disassociated. 

### When I clone a security group to another region, can the source and destination security group share the same name?
Yes.

### Can I clone a security group to another project or region using an API?
Yes. For details, see [CloneSecurityGroup](https://www.tencentcloud.com/document/product/215/39444).

### When I clone a security group to another project or region, will the CVMs associated with the security groups also be cloned?
No. Only the inbound and outbound rules of the security group are cloned. You need to associate CVMs again after cloning.


