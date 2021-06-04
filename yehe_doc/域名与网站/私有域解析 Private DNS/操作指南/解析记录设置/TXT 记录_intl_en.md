## Overview
This document describes how to add a TXT record to identify and describe a domain name.

## Prerequisites
You have created the corresponding private domain.

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create a TXT record or **Records** as shown below:
![](https://main.qcloudimg.com/raw/965b35507b9de90112d57608a95d6405.png)
3. On the **Records** tab, click **Add Record** and enter the following record value information as shown below:
>?You can add up to 20 round-robin DNS records of the same record type for the same host.
>
![](https://main.qcloudimg.com/raw/56a282b329e437794fe04c7c4dee5bf2.png)
 - **Host**: enter a subdomain. For example, when adding a TXT record for `www.dnspod.cn`, you can simply select **www** in the **Host** field. If you want to add a TXT record for `dnspod.cn`, select **@** in the **Host** field.
 - **Record Type**: select **TXT**.
 - **Record Value**: there is no fixed format.
 - **MX Priority**: leave it empty.
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://cloud.tencent.com/act/event/connect-service).



