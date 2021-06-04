## Overview
This document describes how to add a PTR record, through which you can reversely resolve a private IP address to the corresponding private network domain name.
>?You need to configure reverse private domain DNS before adding PTR records. For detailed directions, please see [Reverse DNS and PTR Record Description](https://cloud.tencent.com/document/product/1338/50546).

## Prerequisites
- You have created the corresponding private domain.
- You have configured reverse private domain DNS.

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create a PTR record or **Records** as shown below:
![](https://main.qcloudimg.com/raw/965b35507b9de90112d57608a95d6405.png)
3. On the **Records** tab, click **Add Record** and enter the following record value information as shown below:
![](https://main.qcloudimg.com/raw/c6784df532f337d82a9a4e5eb4e364f5.png)
 - **Host**: the combination of the host and the created domain name (without `in-addr.arpa`) is in the fixed IPv4 format, and you can enter only an integer between 0 and 255 for each IP range.
 - **Record Type**: only **PTR** is supported.
 - **Record Value**: enter the private domain name corresponding to the private IP address.
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://cloud.tencent.com/act/event/connect-service).



