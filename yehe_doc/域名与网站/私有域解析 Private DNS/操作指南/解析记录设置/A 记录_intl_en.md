## Overview
This document describes how to add an A record to point a domain name to an IP address.

## Prerequisites
You have created the corresponding private domain.

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create an A record or **Records** as shown below:
![](https://main.qcloudimg.com/raw/965b35507b9de90112d57608a95d6405.png)
3. On the **Records** tab, click **Add Record** and enter the following record value information as shown below:
>?You can add up to 10 round-robin DNS records of the same record type for the same host.
>
>![](https://main.qcloudimg.com/raw/ce5100ab358d6dcae13e6d0534e0405c.png)
>
> - **Host**: select a subdomain. For example, when adding a record for `www.dnspod.cn`, you can simply select **www** in the **Host** field. If you want to add a record for `dnspod.cn`, select **@** in the **Host** field.	
 - **Record Type**: select **A**.
 - **Record Value**: you can only enter an IPv4 address. For example, if the IPv4 address you want to access is `8.8.8.8`, then enter `8.8.8.8`.
 - **Weight**: it refers to configuring multiple record values for the same host on the DNS server. In this way, when the server responds to DNS queries, all record values will return different DNS results according to the preset weights and distribute the resolved traffic to different servers, so as to implement load balancing. The weight value can be an integer between 1 and 100.
 - **MX Priority**: leave it empty.
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.	

>?If anything goes wrong during this process, please [contact us](https://cloud.tencent.com/act/event/connect-service).	
