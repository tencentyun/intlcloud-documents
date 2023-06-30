## Overview
Security groups are used to manage traffic to and from public and private networks. For the sake of security, most inbound traffic is denied by default. If you selected **Open all ports** or **Open ports 22, 80, 443, 3389 and ICMP protocol** as the template when creating a security group, rules are automatically created and added to the security group to allow traffic on those ports. For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/1119/43431).

This document describes how to add security group rules to allow or reject traffic to and from public or private networks for ECM instances and resources.

## Prerequisites

- You should have an existing security group. If you do not, refer to [Creating a Security Group](https://intl.cloud.tencent.com/document/product/1119/43432) for details.
- You should know which traffic is allowed or rejected for your ECM instance. For more information on security group rules and their use cases, see [Security Group Use Cases](https://intl.cloud.tencent.com/document/product/1119/43446).

## Directions
1. Log in to the ECM console and select **Edge Network** > **[Security Group](https://console.cloud.tencent.com/ecm/safe)** on the left sidebar.
3. On the **Security Group** management page, select **Modify Rule** on the right of the target security group.
4. [](id:Step4)On the **Security Group Rule** tab, click **Inbound Rule** or **Outbound Rule** and select one of the following methods to add a rule:
   - **Method 1**: click **Open all ports** and confirm the operation in the pop-up window. This method is ideal if you do not need custom ICMP rules and all traffic goes through ports 20, 21, 22, 80, 443, and 3389 and the ICMP protocol as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/783d4990e00ca11a94b81d2685741c55.png)
   - **Method 2**: click **Add Rule** and configure the rule in the pop-up window. For more information, see [step 5](#Step5). This method is ideal if you need to set multiple communication protocols such as ICMP as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/afd977f19b1cf101905f53d673b28e33.png)
  - **Method 3**: on the security group rule page, you can modify inbound/outbound rules based on your needs. Select **Inbound Rule** or **Outbound Rule** and add a rule position as needed. Click **Insert** > **Insert Row Above** or **Insert Row Below** on the right of a rule and quickly configure it as instructed in [step 5](#Step5) as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/3799df703b87a1d046fc9d4b13892599.png)
5. [](id:Step5)The main parameters for adding a rule are as detailed below:
   - **Type**: **Custom** is selected by default. You can also choose another system rule template including **Login Windows CVMs (3389)**, **Login Linux CVMs (22)**, **Ping**, **HTTP (80)**, **HTTPS (443)**, **MySQL (3306)**, and **SQL Server (1433)**.
   - **Source** or **Destination**: traffic source (inbound rules) or destination (outbound rules). You need to specify one of the following options:
<table>
<tbody><tr><th>Source/Destination</th><th>Description</th></tr>
<tr><td>A single IPv4 address or an IPv4 range</td><td>In CIDR notation, such as <code>203.0.113.0</code>, <code>203.0.113.0/24</code> or <code>0.0.0.0/0</code>, where <code>0.0.0.0/0</code> indicates all IPv4 addresses will be matched.</td></tr>
</tbody></table>
   - **Protocol Port**: enter the protocol type and port range such as **UDP:53** and **TCP:80,443**.
   - **Policy**: **Allow** or **Refuse**. **Allow** is selected by default.
     - **Allow**: traffic to this port is allowed.
     - **Reject**: data packets will be discarded without any response.
   - **Notes**: a short description of the rule for easier management.
6. Click **Complete**.
7. To add an outbound rule, click **Outbound Rule** and refer to [step 4](#Step4) to [step 5](#Step5).

