Security groups are used to manage whether a Cloud Virtual Machine (CVM) is accessible. You can configure inbound and outbound rules for security groups to specify whether your server can be accessed by or can access other network resources.
Default inbound and outbound rules for security groups are as follows:
- **To ensure data security, the inbound rule for a security group is a rejection policy that denies remote access from external networks.** To make your CVM accessible to external resources, you need to allow the inbound rule for the corresponding port.
- The outbound rule for a security group specifies whether your CVM can access external network resources. If you select **Open All Ports** or **Open Ports 22, 80, 443, and 3389 and ICMP**, the outbound rule for the security group opens the ports to the Internet. If you select a custom security group rule, the outbound rule blocks all ports by default, and you need to set the outbound rule to allow the corresponding port to access external network resources.

## Common Use Cases
This document describes several common use cases for security groups. If any of the following cases meet your requirements, you can set your security groups according to the configuration recommended for the corresponding use case.

### Scenario 1: remotely connecting to a Linux CVM through SSH
**Case**: you have created a Linux CVM and want to remotely connect to the CVM through SSH.
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), set **Type** to **Linux Login** and open TCP port 22 to the Internet to allow Linux login through SSH.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows you to configure the source IP addresses that can remotely access the CVMs through SSH.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Linux login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>TCP: 22</td><td>Allow</td></tr>
</table>

### Scenario 2: remotely connecting to a Windows CVM through RDP
**Case**: you have created a Windows CVM and want to remotely connect to the CVM through Remote Desktop Connection (RDP).
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), set **Type** to **Windows Login** and open TCP port 3389 to the Internet to enable remote login to Windows.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This enables you to configure the source IP addresses that can remotely access the CVMs through RDP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Windows login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>TCP: 3389</td><td>Allow</td></tr>
</table>

### Scenario 3: pinging a CVM from the Internet
**Case**: you have created a CVM and want to check whether the communication between the CVM and other CVMs is normal.
**Solution**: test the connection by using the ping program. Specifically, when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), set **Type** to **Ping** and open Internet Control Message Protocol (ICMP) ports to the Internet to enable other CVMs to gain access to this CVM through ICMP.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows you to configure the source IP addresses that can access this CVM through ICMP.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Ping</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>ICMP</td><td>Allow</td></tr>
</table>

### Scenario 4: remotely logging in to a CVM through Telnet
**Case**: you want to remotely log in to a CVM through Telnet.
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), configure the following security group rule:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>TCP: 23</td><td>Allow</td></tr>
</table>

### Scenario 5: authorizing access to a web service through HTTP or HTTPS
**Case**: you have built a website and want to allow users to access your website through HTTP or HTTPS.
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), configure the following security group rules as required:
- Allow all IP addresses on the Internet to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Allow</td></tr>
</table>
- Allow some IP addresses on the Internet to access this website
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>The IP address or IP address range that is allowed to access your website</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>The IP address or IP address range that is allowed to access your website</td><td>TCP: 443</td><td>Allow</td></tr>
</table>

### Scenario 6: allowing an external IP address to access a specified port
**Case**: you have deployed a service and want the specified service port (such as port 1101) to be accessible externally.
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), set **Type** to **Custom** and open TCP port 1101 to the Internet to allow external resources to access the specified service port.
You can open all IP addresses or a specified IP address (or IP address range) to the Internet as required. This allows the source IP address to access the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>TCP: 1101</td><td>Allow</td></tr>
</table>

### Scenario 7: denying access to a specified port from external IP addresses
**Case**: you have deployed a service and want to block external access to a specified service port (such as port 1102).
**Solution**: when [adding an inbound rule](https://intl.cloud.tencent.com/document/product/215/35513), set **Type** to **Custom**, configure TCP port 1102, and set **Policy** to **Reject** to deny external access to the specified service port.
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: a specified IP address or IP address range</li></ul></td><td>TCP: 1102</td><td>Reject</td></tr>
</table>

### Scenario 8: allowing a CVM to access only a specified external IP address
**Case**: you want your CVM to access only a specified external IP address.
**Solution**: add two outbound security group rules by referring to the following configurations:
- Allow the CVM instance to access a specified public IP address
- Disallow the CVM instance to access any public IP addresses through any protocol

> The rule that permits access should have a higher priority than the rule that denies access.
>
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>The specified public IP address that can be accessed by the CVM</td><td>The required protocol and port</td><td>Allow</td></tr>
<tr><td>Outbound</td><td>Custom</td><td>0.0.0.0/0</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 9: denying a CVM from accessing a specified external IP address
**Case**: you do not want your CVM to access a specified external IP address.
**Solution**: add a security group rule by referring to the following configuration:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>The specified public IP address that you do not want to be accessed by the CVM</td><td>All</td><td>Reject</td></tr>
</table>

### Scenario 10: uploading a file to or downloading a file from a CVM through FTP
**Case**: you want to upload a file to or download a file from a CVM by using an FTP program.
**Solution**: add a security group rule by referring to the following configuration:
<table>
<tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td>0.0.0.0/0</td><td>TCP: 20-21</td><td>Allow</td></tr>
</table>

## Combination of Multiple Scenarios
In an actual scenario, you may want to configure multiple security group rules based on service requirements, for example, configuring inbound or outbound rules at the same time. One CVM may be bound to one or more security groups. When a CVM is bound to multiple security groups, these security groups are matched and executed in descending order of priorities. You can adjust the priorities of these security groups whenever needed. 

