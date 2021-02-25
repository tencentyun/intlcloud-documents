By configuring security groups, you can manage access to a Cloud Virtual Machine (CVM). You can configure inbound and outbound rules for security groups to specify whether your server can be accessed by or can access other network resources.
The default inbound and outbound rules for security groups are as follows:
- **To ensure data security, the inbound rule for a security group is a rejection policy that forbids remote access from external networks.** To enable external network access to your CVM, you need to permit the inbound rule of the corresponding port.
- The outbound rule for a security group specifies whether your CVM can access external network resources. If you select "Open All Ports" or "Open Ports 22, 80, 443, and 3389 and ICMP", the outbound rule for the security group opens all ports to the Internet. If you select a custom security group rule, the outbound rule blocks all ports by default, and you need to configure the outbound rule to allow the corresponding port to access external network resources.

## Common Use Cases
This document describes several common use cases of security groups. If the following cases meet your requirements, you can configure the security groups according to the recommended configurations for the corresponding use cases.

### Scenario 1: Remotely connecting to a Linux CVM through SSH
**Case**: you have created a Linux CVM and want to remotely connect to it through SSH.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Login Linux CVMs(22)** and open TCP port 22 to the Internet to enable Linux login through SSH.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can be remotely connected to through SSH.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Linux login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 22</td><td>Allow</td></tr>
</table>

### Scenario 2: Remotely connecting to a Windows CVM through RDP
**Case**: you have created a Windows CVM and want to remotely connect to it by using Remote Desktop (RDP).
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Login Windows CVMs(3389)** and open TCP port 3389 to the Internet to enable remote login to Windows.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This enables you to configure the source IP addresses of the CVMs that can be remotely connected to through RDP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Windows login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 3389</td><td>Allow</td></tr>
</table>

### Scenario 3: Pinging a CVM on the Internet
**Case**: you have created a CVM and want to test whether its communication with other CVMs is normal.
**Solution**: test the connection by using the ping command. Specifically, when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Ping** and open Internet Control Message Protocol (ICMP) ports to the Internet to enable other CVMs to access this CVM through ICMP.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can access this CVM through ICMP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Ping</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>ICMP</td><td>Allow</td></tr>
</table>

### Scenario 4: Remotely logging in to a CVM through Telnet
**Case**: you want to remotely log in to a CVM by using Telnet.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), configure the following security group rule:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 23</td><td>Allow</td></tr>
</table>

### Scenario 5: Allowing access to a web service through HTTP or HTTPS
**Case**: you have built a website and want to allow users to access your website through HTTP or HTTPS.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), configure the following security group rules as required:
- Allow all public IP addresses to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Allow</td></tr>
</table>
- Allow some public IP addresses to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 443</td><td>Allow</td></tr>
</table>

### Scenario 6: Allowing an external IP address to access a specified port
**Case**: you have deployed a service and want the specified service port (such as port 1101) to be externally accessible.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Custom** and open TCP port 1101 to the Internet to allow external access to the specified service port.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows the source IP address to access the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1101</td><td>Allow</td></tr>
</table>

### Scenario 7: Rejecting access to a specified port by external IP addresses
**Case**: you have deployed a service and want to prevent external access to a specified service port (such as port 1102).
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Custom**, configure TCP port 1102, and set **Policy** to **Reject** to reject external access to the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1102</td><td>Reject</td></tr>
</table>

### Scenario 8: Allowing a CVM to access only a specified external IP address
**Case**: you want your CVM to access only a specified external IP address.
**Solution**: add two outbound security group rules by referring to the following configuration.
- Allow the CVM instance to access a specified external IP address
- Forbid the CVM instance from accessing any public IP addresses through any protocol

> Rules that permit access take priority over those that forbid access.
>
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that can be accessed by the CVM</td><td>Required protocol and port</td><td>Allow</td></tr>
<tr><td>Outbound</td><td>Custom</td><td>0.0.0.0/0</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 9: Prohibiting a CVM from accessing a specified external IP address
**Case**: you do not want your CVM to access a specified external IP address.
**Solution**: add a security group rule by referring to the following configuration.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that you do not want your CVM instance to access</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 10: Uploading or downloading a file from a CVM through FTP
**Case**: you want to upload a file to or download a file from a CVM by using FTP software.
**Solution**: add a security group rule by referring to the following configuration.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td>0.0.0.0/0</td><td>TCP: 20 or 21</td><td>Allow</td></tr>
</table>

## Combination of Multiple Scenarios
In an actual scenario, you may need to configure multiple security group rules based on your business requirements, such as configuring inbound or outbound rules at the same time. One CVM may be bound to one or more security groups. When a CVM is bound to multiple security groups, security groups are matched and executed in descending order of priority. You can adjust the priority of a security group at any time. For information on the priorities of security group rules, see [Security Group Priorities](http://intl.cloud.tencent.com/document/product/213/12452).

