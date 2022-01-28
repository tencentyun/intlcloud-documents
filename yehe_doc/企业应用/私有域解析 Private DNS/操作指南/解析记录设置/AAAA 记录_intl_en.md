## Overview
This document describes how to add an AAAA record to point a domain name to an IPv6 address.

## Prerequisites
You have created the corresponding private domain.

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create an AAAA record or **DNS** as shown below:
![](https://main.qcloudimg.com/raw/c8cd616111485c18ac44ba90c1125704.png)
3. On the **DNS Records** tab, click **Add Record** and enter the following record value information as shown below:
>?You can add up to 10 round-robin DNS records of the same record type for the same host.
>
![](https://main.qcloudimg.com/raw/7e3bcee4e58b180a6370c5b406a0e0b4.png)
 - **Host**: enter a subdomain. For example, when adding a record for `www.dnspod.cn`, you can simply select **www** in the **Host** field. If you want to add a record for `dnspod.cn`, select **@** in the **Host** field.
 - **Record Type**: select **AAAA**.
 - **Record Value**: you can only enter an IPv6 address, such as `ff06:0:0:0:0:0:0:c3`.
 - **Weight**: it refers to configuring multiple record values for the same host on the DNS server. In this way, when the server responds to DNS queries, all record values will return different DNS results according to the preset weights and distribute the resolved traffic to different servers, so as to implement load balancing. The weight value can be an integer between 1 and 100.
 - **MX Priority**: leave it empty.
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://intl.cloud.tencent.com/contact-sales).



