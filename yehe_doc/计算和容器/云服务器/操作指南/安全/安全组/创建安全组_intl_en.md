## Scenario
Security Groups act as virtual firewalls for CVMs. Each CVM instance must associate with at least one security group. By default, each CVM instance has two templates (**Open all ports** and **Open port 22, 80, 443, 3389 and ICMP protocol**) for creating a default security group. For details, refer to [Security Group Overview](https://intl.cloud.tencent.com/document/product/213/12452).

If the default security group does not meet your needs, you can create your own security group as instructed below.


## Directions

1. Log in to the [CVM Console](https://console.cloud.tencent.com/cvm/index).
2. In the left sidebar, select **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)**. The Security Group page then appears.
3. Select a region for the security group. Click **+New**. 
4. In the **Create a security group** page, complete the following configurations:
![](https://main.qcloudimg.com/raw/575b2a589a58aef436bc5208facf4614.png)
 - **Template**: select a template that suits your needs, as shown below:
<table>
	<tr><th>Template</th><th>Description</th><th>Notes</th></tr>
	<tr><td>Open all ports</td><td>All ports are open. May present security issues.</td><td>-</td></tr>
	<tr><td>Open TCP port 22，80，443，3389 and ICMP</td><td>TCP port 22, 80, 443 and 3389, and the ICMP are open. All ports are open internally.</td><td>Suitable for instances with web services.</td></tr>
	<tr><td>Custom</td><td>Creates a blank security group in which rules are added afterwards. For details on how to add rules, refer to <a href="https://intl.cloud.tencent.com/document/product/213/34272">this article</a>.</td><td>-</rd></tr>
</table>
 - **Name**: name of the security group.
 - **Project**: by default, **Default project** is selected. Select a project for better management.
 - **Notes**: a short description for the security group.
5. Click **OK** to create the security group.
If you select **Custom** as the template for your security group, click **Add rules now** to [add security group rules](https://intl.cloud.tencent.com/document/product/213/34272).
