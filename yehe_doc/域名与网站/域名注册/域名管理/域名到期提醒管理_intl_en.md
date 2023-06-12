
## Overview
Tencent Cloud Domains provides the domain expiration reminder feature. If your domain is about to expire, the service will remind you to renew your domain via SMS, email, or other means according to the information you have provided in Tencent Cloud to avoid domain unavailability or high redemption fees caused by domain expiration. This document describes how to enable or disable the domain expiration reminder feature.

>!If you disable the domain expiration reminder feature, Tencent Cloud will no longer send you reminders and you may forget to renew your domain in time, which may lead to domain unavailability or high redemption costs. You are advised to keep the feature enabled.

## About Message Frequencies
Domain expiration reminder push channels and message sending frequencies are as follows:
<table>
<thead>
  <tr>
    <th>Contact Information</th>
    <th>Push Channel</th>
    <th colspan="6">Days Before Domain Expiration (N Days Ago)</th>
    <th colspan="3">Renewal Grace Period (Day N)</th>
    <th colspan="3">Redemption Period (Day N)</th>
    <th>Release</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>Account ID information</td>
    <td>Mobile phone, email, Message Center</td>
    <td>60</td>
    <td>-</td>
    <td>20</td>
    <td>-</td>
    <td>2</td>
    <td>-</td>
    <td>0</td>
    <td>10</td>
    <td>-</td>
    <td>0</td>
    <td>10</td>
    <td>-</td>
    <td>Current day</td>
  </tr>
  <tr>
    <td>Domain identity information</td>
    <td>Mobile phone, email</td>
    <td>30</td>
    <td>-</td>
    <td>10</td>
    <td>-</td>
    <td>1</td>
    <td>-</td>
    <td>-</td>
    <td>20</td>
    <td>-</td>
    <td>-</td>
    <td>20</td>
    <td>-</td>
    <td>-</td>
  </tr>
</tbody>
</table>

>?
>- To modify your account ID information, go to the [CAM console](https://console.intl.cloud.tencent.com/developer).
>- To modify your domain registrant information, see Modifying Registrant Profile.

## Operation Guide
### Disabling domain expiration reminder
1. Log in to the [Domains console](https://console.intl.cloud.tencent.com/domain/manage) and enter the **My Domains** page.
2. On the **My Domains** page, locate the target domain and click **More** > **Disable Expiration Reminder**. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/b60e1d37e14fe176d45b595c11d6d8c5.png)

### Enabling domain expiration reminder
1. Log in to the [Domains console](https://console.intl.cloud.tencent.com/domain/manage) and enter the **My Domains** page.
2. On the **My Domains** page, locate the target domain and click **More** > **Enable Expiration Reminder**. See the figure below:

![](https://qcloudimg.tencent-cloud.cn/raw/6a1b26a909cb931caf5728e714fe47fe.png)


