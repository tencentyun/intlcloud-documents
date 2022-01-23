## Overview
This document describes how to add an SRV record to identify the service used by a server. It is often used for directory management in Microsoft systems.

## Prerequisites
You have created the corresponding private domain. For details, see [Creating Private Domain](https://intl.cloud.tencent.com/document/product/1097/40558).

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create an SRV record or **DNS** as shown below:
![](https://main.qcloudimg.com/raw/965b35507b9de90112d57608a95d6405.png)
3. On the **DNS Records** tab, click **Add Record** and enter the following record value information as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2fd974a599442354bee407a8a1b19fe8.png)
 - **Host**: set it to a value in the format of "service name.protocol type", such as `_sip._tcp`.
 - **Record Type**: select **SRV**.
 - **Record Value**: set it to a value in the format of “priority weight port hostname”. A "." will be automatically appended to the domain name when the record is generated.
An example value is `0 5 5060 sipserver.dnspod.cn`.
 - **Weight**: leave it empty. 
 - **MX Priority**: leave it empty. 
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://intl.cloud.tencent.com/contact-sales).




