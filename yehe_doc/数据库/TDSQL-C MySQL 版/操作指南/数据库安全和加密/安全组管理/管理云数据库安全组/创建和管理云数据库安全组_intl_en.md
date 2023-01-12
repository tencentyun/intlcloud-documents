This document describes how to create and manage security groups for TDSQL-C for MySQL cluster.

## Creating Security Group
1. Log in to the [CVM console](https://console.tencentcloud.com/cvm/instance/index?rid=1)
2. Select **Security Group** on the left sidebar, select a region on the right, and click **Create**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3dJa662_2.png)
3. In the pop-up dialog window, configure the following items, and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WawT696_3.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Template</td>
<td>Select a template based on the service to be deployed on the TencentDB instance in the security group, which simplifies the security group rule configuration, as shown in the table below. </td></tr>
<tr>
<td>Name</td>
<td>Custom name of the security group</td></tr>
<tr>
<td>Project</td>
<td>By default, <strong>Default Project</strong> is selected. Select another project for easier management</td></tr>
<tr>
<td>Remarks</td>
<td>A short description of the security group</td>
<tr>
<td>Advanced Options</td>
<td>You can add tags as needed for the security group in **Advanced Options**, and no tag is selected by default. For details, see <a href="https://www.tencentcloud.com/document/product/1098/50152">Tag Overview</a></td></tr>
<tr>
<td>Display template rule</td>
<td>If the template is selected, you can click **Display template rule** to view the rule details.</td></tr>
</tbody></table>
Table 1:
<table>
<thead><tr><th>Template</th><th>Description</th><th>Remarks</th></tr></thead>
<tbody><tr>
<td>Open all ports</td><td>All ports are opened to the public and private networks. This may expose your database instances to security threats.</td><td>-</td></tr>
<tr>
<td>Open ports 22, 80, 443, and 3389 and the ICMP protocol</td><td>Ports 22, 80, 443, and 3389 and the ICMP protocol are opened to the internet. All ports are opened to the private network.</td><td>This template does not take effect for TencentDB.</td></tr>
<tr>
<td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, see <a href="https://www.tencentcloud.com/document/product/1098/52744">Modifying/Adding Security Group Rules</a></td><td>-</rd></tr>
</table>

## Managing Security Groups
After the security group is created, you can perform management operations for security groups. For detailed directions, see the following steps:
- [Viewing Security Groups](https://intl.cloud.tencent.com/document/product/213/34828)
- [Removing from Security Groups](https://intl.cloud.tencent.com/document/product/213/34830)
- [Cloning Security Groups](https://intl.cloud.tencent.com/document/product/213/34829)
- [Deleting Security Groups](https://intl.cloud.tencent.com/document/product/213/34831)
