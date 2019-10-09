This document describes the common ports used to configure a CVM and the typical use cases of the ports. You can refer to the instructions in this document to configure security group rules.

## Typical Use Cases

By configuring security groups, you can manage the access to a CVM. By default, inbound security group rules deny access to ensure data security. If you want your CVM to be accessed by certain services, you need to configure security group rules to allow the corresponding ports to be accessed.

Typical use cases are shown in the following table.

| Use case                   | Rule direction | Protocol port   | Strategy | Source                                                         |
| -------------------------- | -------- | ---------- | ---- | ------------------------------------------------------------ |
| Allows certain ranges of IP addresses to access TCP port X  | Inbound       | TCP:X     | Allow | Specified ranges of IP addresses (e.g. 192.168.1.0/24)                           |
| Denies certain ranges of IP addresses to access TCP port X  | Inbound       | TCP:Y     | Deny | Specified ranges of IP addresses (e.g. 192.168.1.0/24)                           |
| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows using RDP to remotely connect to a Windows instance    | Inbound       | TCP:3389    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses(0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows remote login using Telnet           | Inbound       | TCP:23    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows pinging a CVM in the public network            | Inbound       | ICMP    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows using FTP to upload or download files            | Inbound       | TCP:20-21    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows using a CVM as the web server            | Inbound       | TCP:80    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |
| Allows using a CVM as the MySQL server            | Inbound       | TCP:3306    | Allow | Select one of the following to be the source based on your needs:<li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)| Allows using SSH to remotely connect to a Linux instance    | Inbound       | TCP:22    | Allow | <li>All IP addresses (0.0.0.0/0)</li><li>Specified ranges of IP addresses (e.g., 192.168.1.0/24)</li> |


## Operation Example
Take using SSH to remotely connect to a Linux instance as an example. You need to open the protocol port TCP:22 when configuring the inbound rules:
1. Go to the security group rule configuration page. For details, see [Modify Security Group Rules] (https://intl.cloud.tencent.com/document/product/213/18197#.E4.BF.AE.E6.94.B9.E5.AE.89.E5.85.A8.E7.BB.84.E8.A7.84.E5.88.99).
2. In the “Add Inbound Rule” window, select type and source, open protocol port TCP:22, set the policy to “Allow,” and click **Complete**. 
![](https://main.qcloudimg.com/raw/86c1541282e7ac6d02e817c006270a00.png)
3. After you complete the configuration, the new security group rule to allow remote login to Linux instances via SSH is as shown in the red box below.
![](https://main.qcloudimg.com/raw/17325802d9829695568132ba9ce5ccbb.png)

For more information on the configuration of security group rules and common server ports, see [Security Group Limits] (https://intl.cloud.tencent.com/document/product/213/12453) or [Common Server Ports] (https://intl.cloud.tencent.com/document/product/213/12451).

