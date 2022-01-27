## Overview
This document describes how to add an MX record. If you want to set up your mailbox so that it can receive emails, you need to add an MX record.

## Prerequisites
You have created the corresponding private domain.

## Directions
1. Log in to the [Private DNS console](https://console.cloud.tencent.com/privatedns/) and click **Private Domain List** on the left sidebar to enter the private domain list.
2. In the **Private Domain List**, click the name of the private domain for which you need to create an MX record or **DNS** as shown below:
![](https://main.qcloudimg.com/raw/0e4203f75677414eb5416bfad61347ca.png)
3. On the **DNS Records** tab, click **Add Record** and enter the following record value information as shown below:
![](https://main.qcloudimg.com/raw/04ee4d6e590dfb200f654caec1f59669.png)
 - **Host**: enter a subdomain, which is usually "@" or "mail". For example, if **Host** is "@", then the email address will be `xxx@qq.com`; if **Host** is "mail", then the email address will be `xxx@mail.qq.com`.
 - **Record Type**: select **MX**.
 - **Record Value**: it can be either a domain name or an IP address.
    - If the value is a domain name, the domain name should have an A record, and after the record is generated, a period (.) will be automatically added after it.
     For example, to set an MX record with the value `mail.qq.com`, you need to add an A record with the host "mail".
    - If the value is an IP address, directly enter the mail server IP, and after the record is generated, a period (.) will also be automatically added after it.
 - **Weight**: leave it empty. 
 - **MX Priority**: the smaller the value, the higher the priority.
 >!The value of MX priority can only be a positive multiple of 5 and less than or equal to 50.
 - **TTL**: it is the cache time and 300s by default. The smaller the value, the faster the change to the record will take effect. You can enter an integer between 1 and 86400.
4. Click **Save**.

>?If anything goes wrong during this process, please [contact us](https://intl.cloud.tencent.com/contact-sales).



