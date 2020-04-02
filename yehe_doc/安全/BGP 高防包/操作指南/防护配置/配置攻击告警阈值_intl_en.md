## Introduction
When attacks against your Anti-DDoS Pro resources start/end, and your Anti-DDoS Pro IPs are blocked/unblocked, you will get notifications in Message Center or via SMSs or emails. Configuring proper alarm thresholds can help you know about the attack instantly. And this feature can also help prevent mis-alarming caused by normal business operations that bring traffic rush (for example, data synchronization). For more information about how you can receive the alarm messages, please refer to [Security Event Notification Settings](https://intl.cloud.tencent.com/document/product/1029/31766).
## Configuring DDoS Attack Alarm Threshold
Scenario: When Anti-DDoS Pro detects that the inbound traffic bandwidth of the Single IP instance “bgp-000005w1” is over 1,000 Mbps, the system will send DDoS attack alarm message to the specific user group.
>To set the attack alarm threshold, make sure you have enabled DDoS protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2) and choose **Anti-DDoS Pro** -> **Resource List** in the left sidebar to enter the Anti-DDoS Pro page. Click **Single IP Instance** to find the instance “bgp-000005w1”, and then click **Protection Configuration** in the line of the instance.
![](https://main.qcloudimg.com/raw/f4303e9b72ea23c9907705c8d9b2e0b5.png)
2. Enter the **DDoS Protection** page, select the alarm metric **Inbound Traffic Bandwidth** in the drop-down list to the right of the DDoS attack alarm threshold, and set the threshold to 1000 Mbps.
>The DDoS attack alarm threshold is **Not Set** by default. Available alarm metrics include **Inbound Traffic Bandwidth** and **Cleansing Traffic**.
>
![](https://main.qcloudimg.com/raw/a5f2a0939817b28eb2d1423a396333c4.png)

## Configuring CC Attack Alarm Threshold
Scenario: CC Protection is enabled for the Single IP instance “bgp-000006i9”. When the CC protection bandwidth exceeds 2000 QPS, alarm messages will be sent to the specific user group.
>To set the attack alarm threshold, make sure you have enabled CC protection.

1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgpip_v2) and choose **Anti-DDoS Pro** -> **Protection Configuration**. On the **CC Protection** tab, select **Single IP Instance** -> **CC Protection**.
. Click **CC Protection** and set the threshold to 2,000 QPS for the CC attack alarm threshold.
![](https://main.qcloudimg.com/raw/8471af6557ca19765788946c06109381.png)
