
### Why does a security group have a reject rule by default?

Security group rules take effect sequentially from top to bottom. If an allow rule that was previously set takes effect, other rules will be rejected by default. If this allow rule opens all ports to Internet, the last reject rule will not take effect. We provide this default setting due to security concerns.

### How can I adjust the priority of a security group?

For more information, see [Adjusting Security Group Priority](https://intl.cloud.tencent.com/document/product/213/35375).

### If I bind an incorrect security group to an instance, what impact will this have on the instance? How can I fix this problem?

**Potential problems**

- You may fail to remotely connect to a Linux instance over SSH or a Windows instance via remote desktop.
- You may fail to remotely ping the public IP and private IP addresses of the CVM instance in this security group.
- You may fail to access over HTTP the web services exposed by the CVM instance in this security group.
- The CVM instance in this security group may fail to access Internet services.

**Solutions**

- If any of the aforementioned problems occur, you can go to **Security Groups** on the Console and modify the security group rule. For example, you can change the rule to "bind only all-ports-open security groups by default".
- For more information on how to set a security group rule, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

### What do the security group direction and policy mean?

There are outbound and inbound security group directions. The outbound direction filters the outbound traffic of the CVM instance, whereas the inbound direction filters the inbound traffic of the CVM instance.
Security group policies are divided into those that **allow** and **refuse** traffic.

### In which order do the security group policies take effect?

Security group policies take effect sequentially from top to bottom when traffic flows through the security group. Once the traffic matches a policy, the policy will take effect immediately.

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

### Can a security group be cloned across different users?

No. This feature is currently not supported.

### Is there any Tencent Cloud API that supports the cloning of a security group across projects and regions?

While MC support is provided to help customers who use the Console, no Tencent Cloud API can be directly used for this purpose at the moment. You can use the original Tencent Cloud APIs for batch importing and exporting of security group rules to indirectly clone a security group across projects and regions.

### When I clone a security group across projects and regions, will CVM instances managed by the security group also be copied?

No. When a security group is cloned across regions, only the inbound and outbound rules of the original security group will be copied. Therefore, you need to bind CVM instances to the security group separately.

### What is a security group?
A security group is a virtual firewall that features stateful data packet filtering. It is used to configure the network access control of CVM, Cloud Load Balancer, TencentDB, and other instances while controlling their outbound and inbound traffic. It is an important means of network security isolation.

Each CVM instance is bound to at least one security group, which must be specified when the instance is created. CVM instances are interconnected in the same security group but cannot communicate with CVM instances across security groups. However, you can authorize the interconnection between two security groups. For more information, see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

### Why do I need to choose a security group when creating CVM instances?
Before creating CVM instances, you must choose a security group to partition the security domains of the application environment and authorize the security group rules to properly implement network security isolation.

### What should I do when I create CVM instances if I have not created a security group?
In this case, you can create a security group.
A security group supports the following rules. You can open IPs and ports as needed.
- ICMP: opens to the ICMP protocol and allows the pinging of the server over the public network.
- TCP:80: opens port 80 and allows access to Web services over HTTP.
- TCP:22: opens port 22 and allows a remote connection to Linux CVMs over SSH.
- TCP:443: opens port 443 and allows access to Web services over HTTPS.
- TCP:3389: opens port 3389 and allows a remote connection to Windows CVMs over RDP.
- Open the private network: opens to the private network and allows private network access among different cloud resources (IPv4).


### In what situations will the default security group rule be used to a security group?
The default security group rule will be used in the following situations:
- If you purchase and create a CVM instance with **Custom Configuration**, a default security group that uses the default security rule will be created for you automatically. Its inbound rule opens all ports and its outbound rule allows all accesses.
However, for security reasons, we recommend you associate your CVM with a new security group that only opens ports when absolutely necessary to avoid unnecessary security risks.
- You can choose a template when creating a security group on the CVM Console. Currently, supported templates include Windows login, Linux login, Ping, HTTP(80) and HTTPS(443).
