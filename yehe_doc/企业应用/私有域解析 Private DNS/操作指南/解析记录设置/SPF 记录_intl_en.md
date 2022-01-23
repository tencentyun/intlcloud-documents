## Overview
This document describes how to add an SPF record to specify the server for sending emails. This is an efficient anti-spam solution.

## Prerequisites
You have created the corresponding private domain. For details, see [Creating Private Domain](https://intl.cloud.tencent.com/document/product/1097/40558).

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create an SPF record or **DNS** as shown below:
![](https://main.qcloudimg.com/raw/965b35507b9de90112d57608a95d6405.png)
3. On the **DNS Records** tab, click **Add Record** and enter the following record value information as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/26e7e57467802ae9becc9dabaf685278.png)
 - **Host**: enter a subdomain. For example, when adding an SPF record for `www.123.com`, you can simply select **www** in the **Host** field. If you want to add an SPF record for `123.com`, select **@** in the **Host** field.
 - **Record Type**: select **SPF**.
 - **Record Value**: for example, `v=spf1 include:spf.mail.qq.com ~all` indicates that only the IP addresses in the A record and MX record of this domain have permission to send emails using this domain.
 - **Weight**: leave it empty. 
 - **MX Priority**: leave it empty. 
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://intl.cloud.tencent.com/contact-sales).




