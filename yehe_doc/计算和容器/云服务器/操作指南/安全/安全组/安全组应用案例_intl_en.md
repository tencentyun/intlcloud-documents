Security groups can manage the access to CVMs. You can configure inbound and outbound rules for security groups to specify whether your server can be accessed by or can access other network resources.
The default inbound and outbound rules for security groups are as follows:
- **To ensure data security, the inbound rule for a security group is a rejection policy that forbids remote access from external networks.** To enable public access to your CVM, you need to open the corresponding port to the Internet in the inbound rule.
- The outbound rule for a security group specifies whether your CVM can access external network resources. If you select **Open all ports** or **Open ports 22, 80, 443, and 3389 and the ICMP protocol**, the outbound rule for the security group opens all ports to the Internet. If you select a custom security group rule, the outbound rule blocks all ports by default, and you need to configure the outbound rule to open the corresponding port to the Internet.

## Common Use Cases
This document provides several common use cases of security groups. You can directly use its recommended security group configurations if a use case meets your requirements.

### Scenario 1: remotely connecting to a Linux CVM via SSH
**Case**: you have created a Linux CVM and want to remotely connect to it via SSH.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Login Linux CVMs(22)**, enter WebShell proxy IP address for **Source**, and open TCP port 22 to the Internet to enable Linux login via SSH.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can be remotely connected to through SSH.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Linux login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li>
<li>WebShell proxy IP addresses: as detailed in <a href="https://cloud.tencent.com/document/product/213/52645">WebShell Proxy IP Addresses Updates</a>
</li>
<li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP:22</td><td>Allow</td></tr>
</table>

### Scenario 2: remotely connecting to a Windows CVM through RDP
**Case**: you have created a Windows CVM and want to remotely connect to it by using Remote Desktop (RDP).
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Login Windows CVMs(3389)**, enter the WebRDP proxy IP addresses for **Source**, and open TCP port 3389 to the Internet to enable remote login to Windows.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This enables you to configure the source IP addresses of the CVMs that can be remotely connected to via RDP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Windows login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li>
<li>WebRDP proxy IP addresses:
 <ol>81.69.102.0/24</ol>
<ol>106.55.203.0/24</ol>
<ol>101.33.121.0/24</ol>
<ol>101.32.250.0/24</ol>
</li>
<li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP:3389</td><td>Allow</td></tr>
</table>

### Scenario 3: pinging a CVM on the Internet
**Case**: you have created a CVM and want to test whether its communication with other CVMs is normal.
**Solution**: test the connection by using the `ping` command. Specifically, when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Ping** and open Internet Control Message Protocol (ICMP) ports to the Internet to enable other CVMs to access this CVM through ICMP.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows you to configure the source IP addresses of the CVMs that can access this CVM through ICMP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Ping</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>ICMP</td><td>Allow</td></tr>
</table>

### Scenario 4: remotely logging in to a CVM through Telnet
**Case**: you want to remotely log in to a CVM by using Telnet.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), configure the following security group rule:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 23</td><td>Allow</td></tr>
</table>

### Scenario 5: allowing access to a web service through HTTP or HTTPS
**Case**: you have built a website and want to allow access to your website through HTTP or HTTPS.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), configure the following security group rules as required:
- Allow all public IP addresses to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Allow</td></tr>
</table>
- Allow some public IP addresses to visit this website.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 443</td><td>Allow</td></tr>
</table>

### Scenario 6: allowing an external IP address to access a specified port
**Case**: you have deployed a service and want the specified service port (such as port 1101) to be externally accessible.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Custom** and open TCP port 1101 to the Internet to allow external access to the specified service port.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows the source IP address to access the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1101</td><td>Allow</td></tr>
</table>

### Scenario 7: rejecting an external IP address to access a specified port
**Case**: you have deployed a service and want to prevent external access to a specified service port (such as port 1102).
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/213/34272), set **Type** to **Custom**, configure the TCP port 1102, and set **Policy** to **Reject**, so that external services cannot access the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1102</td><td>Reject</td></tr>
</table>

### Scenario 8: allowing a CVM to access only a specified external IP address
**Case**: you want your CVM to access only a specified external IP address.
**Solution**: add two outbound security group rules as follows.
- Allow the CVM instance to access a specified external IP address.
- Forbid the CVM instance from accessing any public IP addresses via any protocol.

>! The first rule takes priority over the second.
>
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that the CVM can access</td><td>Required protocol and port number</td><td>Allow</td></tr>
<tr><td>Outbound</td><td>Custom</td><td>0.0.0.0/0</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 9: prohibiting a CVM from accessing a specified external IP address
**Case**: you do not want your CVM to access a specified external IP address.
**Solution**: add a security group rule as follows.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that your CVM instance cannot access</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 10: uploading or downloading a file from a CVM through FTP
**Case**: you want to allow uploads and downloads over FTP.
**Solution**: add a security group rule as follows.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td>0.0.0.0/0</td><td>TCP: 20 to 21</td><td>Allow</td></tr>
</table>

## Multi-scenario Configurations
You can configure multiple security group rules to meet your business requirements. For example, both inbound and outbound runes can be simultaneously configured. A CVM instance can be bound to one or multiple security groups. When it is bound to multiple security groups, the security group rules will be matched sequentially from top to bottom. You can adjust the priorities of security groups at any time. For more information about the priorities, see [Rule Priorities](https://intl.cloud.tencent.com/document/product/213/12452).



