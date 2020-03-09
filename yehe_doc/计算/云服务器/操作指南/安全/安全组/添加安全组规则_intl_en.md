## Scenario
Security groups are used to manage traffic to and from public and private networks. For the sake of security, most inbound traffic is denied by default. If you selected **Open all ports** or **Open port 22, 80, 443, 3389 and ICMP protocol** as the template when creating a security group, rules are automatically created and added to the security group to allow traffic on those ports. For details, refer to [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).

This article describes how to add security group rules to allow or ban traffic to and from public or private networks.

## Notes

- Security group rules support IPv4 and IPv6 rules.
- **Open all ports** allows both IPv4 and IPv6 traffic.

## Prerequisites
- You should have an existing security group. If you do not, refer to [Create a Security Group](https://intl.cloud.tencent.com/document/product/213/34271) for details.
- You should have a clear understanding about which traffic is allowed or banned for your CVM instance. For more information on security group rules and their use cases, refer to [Security group use cases](https://intl.cloud.tencent.com/document/product/213/32369).

## Directions
1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**. The Security Group page then appears.
3. On the **Security Group** page, select a region, and find the security group for which you want to set rules.
4. Locate the desired security group and click the corresponding **Modify Rules** button to go to the Security Group Rule page.
5. <span id="step05">Click **Inbound rules** and choose one of the following methods to add rules.</span>
> The following instructions use method two **Add a rule** as an example.
>
 - Open all ports: this method is ideal if you do not need custom ICMP rules and all traffic goes through ports 20, 21, 22, 80, 443, and 3389 and the ICMP protocol.
 - Add a rule: this method is ideal if you need to use multiple protocols and ports other than those mentioned above.
6. Click **Add a Rule** to bring up the **Add Inbound Rule** window. 
Configure the following parameters:
 - Type: by default, **Custom** is selected. You can select other types such as **Login Windows CVMs (3389)**, **Login Linux CVMs (22)**, **Ping**, **HTTP (80)**, **HTTPS (443)**, **MySQL (3306)**, and **SQL Server (1433)**.
 - **Source** or **Destination**: traffic origin (inbound rules) or target (outbound rules). You can use one of the following to define Source or Destination:
<table>
	<tr><th>Source or Destination</th><th>Description</th></tr>
	<tr><td>IPv4 addresses or ranges</td><td> in CIDR format<code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>. <code>0.0.0.0/0</code> indicates all IPv4 addresses.</td></tr>
	<tr><td>IPv6 addresses or ranges</td><td> in CIDR format, such as<code>FF05::B5</code>, <code>FF05:B5::/60</code>, <code>::/0</code> or <code>0::0/0</code>. <code>::/0</code> or <code>0::0/0</code> indicates all IPv6 addresses.</td></tr>
	<tr><td>ID of referenced security group. You can reference the ID of:<ul  style="margin: 0;"><li>Current security group</li><li>Other security group</li></ul>
</td><td><ul  style="margin: 0;"><li>Current security group: CVMs associated with the current security group.</li><li>Other security group: ID of another security group in the same region that belongs to the same project.</li></ul>
</td></tr>
	<tr><td>Reference IP address objects or IP group objects in a Parameter Template.</td><td>-</td></tr>
</table>
 - Protocol port: `protocl:port`. You can also reference protocol/port or protocol/port groups in a Parameter Template.
 - Policy: Allow or Refuse. By default, Allow is selected.
    - Allow: traffic to this port is allowed.
    - Refuse: data packets are dropped without any response.
 - Remarks: a short description of the security group rule.
7. <span id="step07">Click **Complete** to finish adding the rule.</span>
8. To add an outbound rule, click **Outbound rule** and refer to [Step 5](#step05) to [Step 7](#step07).
