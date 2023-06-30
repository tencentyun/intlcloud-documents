## Overview

Security groups act as virtual firewalls for ECM instances. Each ECM instance must be associated with at least one security group. If you haven't created a security group when creating an ECM instance, Tencent Cloud provides two templates (**Open all ports** and **Open ports 22, 80, 443, and 3389 and ICMP protocol**) for quick security group creation. For more information, see [Security Group](https://intl.cloud.tencent.com/document/product/1119/43431).

This document describes how to create a security group in the ECM console.

## Directions

1. Log in to the ECM console and select **Edge Network** > **[Security Group](https://console.cloud.tencent.com/ecm/safe)** on the left sidebar.
3. On the **Security Group** management page, click **Create**.
4. In the **Create ECM Security Group** pop-up window, configure the options as shown below:
   ![](https://qcloudimg.tencent-cloud.cn/raw/5150a861044b0f1acf692205bcb53e2e.png)
   - **Template**: select an appropriate template based on the service to be deployed in the ECM instance in the security group, which simplifies the security group rule configuration, as shown below:
<table>
<tbody><tr><th>Template</th><th>Description</th><th>Scenario</th></tr>
<tr><td>Open all ports</td><td>All ports are open. May present security issues.</td><td>-</td></tr>
<tr><td>Open ports 22, 80, 443, and 3389 and ICMP protocol</td><td>Ports 22, 80, and 443 and 3389, and the ICMP protocol are open. All ports are open internally.</td><td>Suitable for instances with web services.</td></tr>
<tr><td>Custom</td><td>You can create a security group and then add custom rules. For detailed directions, see <a href="https://intl.cloud.tencent.com/document/product/1119/43440" target="_blank">Adding Security Group Rule</a>.</td><td>-</td></tr>
</tbody></table>
   - **Name**: name of the security group.
   - **Notes**: a short description of the security group.
   - **Advanced Settings**: you can add tags for the security group after expanding.
   - **Display Template Rules**: you can view the existing rules in the security group after expanding.
5. Click **OK**.
