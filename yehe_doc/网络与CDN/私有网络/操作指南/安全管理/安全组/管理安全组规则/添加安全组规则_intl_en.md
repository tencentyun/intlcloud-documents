## Operation Scenario
Security groups are used to determine whether to permit access requests from the Internet or private networks. For security considerations, access denial is adopted in the inbound direction in most cases. If you select the "Open all ports to the Internet" or "Open ports 22, 80, 443, and 3389 and the ICMP protocol to the Internet" template when creating a security group, the system will automatically add security group rules for some communication ports based on the selected template. 

This document describes how to add security group rules to allow or forbid CVMs in a security group to access the Internet or VPC instances.

## Notes

- Security group rules are divided into IPv4 and IPv6 security group rules.
- **Open all ports** is applicable to both IPv4 and IPv6 security group rules.

## Prerequisites
- You have created a security group. 
- You know what Internet or private network access requests need to be permitted or rejected for your CVM instance. For more use cases of security group rule settings, see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/215/35519).

## Steps
1. Log in to [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, click **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** to enter the security group management page.
3. On the security group management page, choose **Region**, and locate the row of the security group for which you want to set rules.
4. In the operation column, click **Modify Rules**.
5. <span id="step05">On the security group rule page, click **Inbound rules**, and select one of the following modes based on your actual needs to complete the operation.</span>
> The following operation examples use mode 2 (adding rules).
>
 - Mode 1 (open all ports): is applicable to scenarios in which ICMP protocol rules do not need to be set and operations can be done through ports 22, 3389, 80, 443, 20, and 21, as well as the ICMP protocol.
 - Mode 2 (adding rules): is applicable to scenarios in which multiple communication protocols, such as ICMP, need to be set.
6. In the **Add Inbound Rules** window that appears, set rules.
The main parameters required for adding a rule are as follows:
 - Type: the default value is "Custom". You can also select another system rule template, such as "Windows login", "Linux login", "Ping", "HTTP (80)", or "HTTPS (443)".
 - Source/Destination: the source (inbound rules) or destination (outbound rules) of traffic. Choose one of the following options:
<table>
	<tr><th>Specified Source/Destination</th><th>Description</th></tr>
	<tr><td>An IPv4 address or IPv4 address range</td><td>Specify it in CIDR notation (for example, <code>203.0.113.0</code>, <code>203.0.113.0/24</code>, or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates that all IPv4 addresses will be matched).</td></tr>
	<tr><td>An IPv6 address or IPv6 address range</td><td>Specify it in CIDR notation (for example, <code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code>, or <code>0::0/0</code>, where <code>::/0</code> or <code>0::0/0</code> indicates that all IPv6 addresses will be matched).</td></tr>
	<tr><td>Import security group ID: you can import the following security group IDs:<ul  style="margin: 0;"><li>Security group ID</li><li>Another security group</li></ul>
</td><td><ul  style="margin: 0;"><li>The current security group refers to the CVMs associated with the security group.</li><li>Another security group refers to the ID of another security group under the same project in the same region.</li></ul>
</td></tr>
	<tr><td>Import the IP address object or IP address group object in the <a href="https://intl.cloud.tencent.com/document/product/215/31867">parameter template</a>.</td><td>-</td></tr>
</table>
 - Protocol port: enter the protocol type and port range, or import a protocol port or protocol port group in the [parameter template](https://intl.cloud.tencent.com/document/product/215/31867).
 - Policy: the default value is "Permit".
    - Permit: permit access requests over the port.
    - Reject: discard data packets directly without returning any response.
 - Remarks: briefly describe the rule to facilitate future management.
7. <span id="step07">Click **Finish**. Inbound rules are added to the security group.</span>
8. On the security group rule page, click **Outbound Rules**, and add outbound rules to the security group by referring to [Step 5](#step05) to [Step 7](#step07).
