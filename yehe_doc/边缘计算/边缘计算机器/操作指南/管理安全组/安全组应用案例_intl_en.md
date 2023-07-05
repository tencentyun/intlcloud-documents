By configuring security groups, you can manage access to an ECM instance. You can configure inbound and outbound rules for security groups to specify whether your instance can be accessed by or can access other network resources.
The default inbound and outbound rules for security groups are as follows:

- **To ensure data security, the inbound rule for a security group is a rejection policy that forbids remote access from external networks.** To enable public access to your ECM instances, you need to open the corresponding port to the internet in the inbound rule.
- The outbound rule for a security group specifies whether your ECM instance can access external network resources. If you select **Open all ports** or **Open ports 22, 80, 443, and 3389 and the ICMP protocol**, the outbound rule for the security group opens all ports to the Internet. If you select a custom security group rule, the outbound rule blocks all ports by default, and you need to configure the outbound rule to open the corresponding port to the Internet.

## Common Use Cases

This document provides several common use cases of security groups. You can directly use its recommended security group configurations if a use case meets your requirements.

### Scenario 1: remotely connecting to Linux ECM instance over SSH
**Case**: you have created a Linux ECM instance and want to remotely connect to it over SSH.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), set **Type** to **Linux login** and open TCP port 22 to the Internet to enable Linux login via SSH.
You can open all IPs or a specified IP (or IP range) to the internet as required. This enables you to configure the source IPs that can remotely connect to the ECM instance over SSH.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Linux Login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 22</td><td>Allow</td></tr>
</tbody></table>

### Scenario 2: remotely connecting to Windows ECM instance over RDP
**Case**: you have created a Windows ECM instance and want to remotely connect to it over RDP.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), set **Type** to **Windows Login** and open TCP port 3389 to the Internet to enable remote login to Windows.
You can open all IPs or a specified IP (or IP range) to the internet as required. This enables you to configure the source IPs that can remotely connect to the ECM instance over RDP.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Windows Login</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 3389</td><td>Allow</td></tr>
</tbody></table>

### Scenario 3: pinging server on internet
**Case**: you have created an ECM instance and want to test whether it can communicate with other ECM instances normally.
**Solution**: test the connection by using the `ping` command. Specifically, when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), set **Type** to **Ping** and open Internet Control Message Protocol (ICMP) ports to the internet to enable other ECM instances to access this instance over ICMP.
You can open all IPs or a specified IP (or IP range) to the internet as required. This allows you to configure the source IP addresses that can access this ECM instance over ICMP.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Ping</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>ICMP</td><td>Allow</td></tr>
</tbody></table>


### Scenario 4: remotely logging in to ECM instance over Telnet
**Case**: you want to remotely log in to an ECM instance over Telnet.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), configure the following security group rule:
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 23</td><td>Allow</td></tr>
</tbody></table>

### Scenario 5: allowing access to a web service through HTTP or HTTPS

**Case**: you have built a website and want to allow access to your website through HTTP or HTTPS.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), configure the following security group rules as required:
- Allow all public IP addresses to access this website
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>0.0.0.0/0</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>0.0.0.0/0</td><td>TCP: 443</td><td>Allow</td></tr>
</tbody></table>
- Allow some public IP addresses to visit this website.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>HTTP (80)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 80</td><td>Allow</td></tr>
<tr><td>Inbound</td><td>HTTPS (443)</td><td>IP address or IP range that is allowed to access your website</td><td>TCP: 443</td><td>Allow</td></tr>
</tbody></table>

### Scenario 6: allowing an external IP address to access a specified port

**Case**: you have deployed a service and want the specified service port (such as port 1101) to be externally accessible.
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), set **Type** to **Custom** and open TCP port 1101 to the Internet to allow external access to the specified service port.
You can open all IP addresses or a specified IP address (or IP range) to the Internet as required. This allows the source IP address to access the specified service port.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1101</td><td>Allow</td></tr>
</tbody></table>

### Scenario 7: rejecting an external IP address to access a specified port
**Case**: you have deployed a service and want to prevent external access to a specified service port (such as port 1102).
**Solution**: when [adding a security group rule](https://intl.cloud.tencent.com/document/product/1119/43440), set **Type** to **Custom**, configure the TCP port 1102, and set **Policy** to **Reject** to reject external access to the specified service port.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td><ul style="margin: 0;"><li>All IP addresses: 0.0.0.0/0</li><li>Specified IP address: enter your specified IP address or IP range</li></ul></td><td>TCP: 1102</td><td>Reject</td></tr>
</tbody></table>

### Scenario 8: allowing ECM instance to access only specified external IP
**Case**: you want your ECM instance to access only a specified external IP address.
**Solution**: add two outbound security group rules as follows.
- Allow the instance to access a specified external IP address.
- Forbid the instance from accessing any public IP addresses through any protocol.

> !The first rule takes priority over the second.

<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that the ECM instance can access</td><td>Required protocol and port number</td><td>Allow</td></tr>
<tr><td>Outbound</td><td>Custom</td><td>0.0.0.0/0</td><td>All</td><td>Reject</td></tr>
</tbody></table>

### Scenario 9: prohibiting ECM instance from accessing specified external IP

**Case**: you don't want your ECM instance to access a specified external IP address.
**Solution**: add a security group rule as follows.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Outbound</td><td>Custom</td><td>Specified public IP address that your instance cannot access</td><td>All</td><td>Reject</td></tr>
</tbody></table>

### Scenario 10: uploading or downloading a file over FTP

**Case**: you want to allow uploads and downloads over FTP.
**Solution**: add a security group rule as follows.
<table>
<tbody><tr><th>Direction</th><th>Type</th><th>Source</th><th>Protocol Port</th><th>Policy</th></tr>
<tr><td>Inbound</td><td>Custom</td><td>0.0.0.0/0</td><td>TCP: 20 to 21</td><td>Allow</td></tr>
</tbody></table>

## Multi-Scenario Configurations

You can configure multiple security group rules to meet your business requirements. For example, both inbound and outbound runes can be simultaneously configured. An ECM instance can be bound to one or multiple security groups. When it is bound to multiple security groups, the security group rules will be matched sequentially from top to bottom. You can adjust the priorities of security groups at any time. For more information about the priorities, see [Rule Priorities](https://intl.cloud.tencent.com/document/product/1119/43431).



