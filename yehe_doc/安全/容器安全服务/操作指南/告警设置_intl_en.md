This document describes how to configure alert policies for image security events and runtime security events.

## Prerequisites
Make sure you have subscribed to TCSS in "Message Center - Subscription Management", which can be set by clicking [here](https://console.cloud.tencent.com/message/subscription).

## Event types
The following table lists the event types, default alerting period, and alert triggers in alert policies: 

| Event Type | Default Alerting Period | Default Alert Triggers             |
| -------- | ------------ | ---------------------- |
| Vulnerability | All day         | Critical                   |
| Virus and trojan | All day         | Critical, High, Medium, Low |
| Sensitive data | All day         | Critical, High, Medium, Low |
| Container escape | All day         | -                      |
| Abnormal process | All day         | Failed to block, Alert         |
| File tampering | All day         | Failed to block, Alert         |
| Reverse shell | All day         | -         |
| Virus scanning | All day         | -         |

## Directions
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Alert Policies** on the left sidebar.
2. On the **Alert Policies** page, toggle on the **Alerting status** switch.
![](https://qcloudimg.tencent-cloud.cn/raw/c0217985d748ca8aaeaa1dc08258fde4.png)
3. After enabling the alert policy mode, click ![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png) to select the alerting period (**All day** or custom).
 - Select ![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png) on the left of **All day** to send alert notifications all day.
![](https://qcloudimg.tencent-cloud.cn/raw/3a3547a30818061f1bfa8001901ca776.png) 
 - Select ![](https://main.qcloudimg.com/raw/f03c476d56766d47f8a37addc74c7d6b.png) on the left of the custom time box, select the start time and end time, and click **OK** to send alert notifications during the period.
![](https://qcloudimg.tencent-cloud.cn/raw/088b19e7691915ae7eb4af20543cda59.png)
