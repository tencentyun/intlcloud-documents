## Application Scenarios
When attacks against your Anti-DDoS Pro resources start/end, and your Anti-DDoS Pro IPs are blocked/unblocked, you will get notifications via internal messages, SMSs, emails, or WeChat. Configuring proper alarm thresholds can help you know about the attack instantly. And this feature can also help prevent mis-alarming caused by normal business operations that bring traffic rush (for example, data synchronization). For more information about how you can receive the alarm messages, please refer to [Security Event Notification Settings](https://cloud.tencent.com/document/product/1021/31495).
## Configuring DDoS Attack Alarm Threshold
Scenario: When Anti-DDoS Pro detects that the inbound traffic bandwidth of the Single IP instance “bgp-000005w1” is over 1,000 Mbps, the system will send DDoS attack alarm message to the specific user group.
>To set the attack alarm threshold, make sure you have enabled DDoS protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Resource List** in the left sidebar to enter the Anti-DDoS Pro page. Click **Single IP Instance** to find the instance “bgp-000005w1”, and then click the operation item **Protection Configuration** in the line of the instance.
![](https://main.qcloudimg.com/raw/2ede4561a7b8cd9c2e9a4468ef8ff5b5.png)
2. Enter the **Protection Policy** page and locate to “DDoS Protection” section. Select the alarm metric **Inbound Traffic Bandwidth** in the drop-down list to the right of the DDoS attack alarm threshold, and set the threshold to 1,000 Mbps.
>The DDoS attack alarm threshold is **Not Set** by default. Available alarm metrics include **Inbound Traffic Bandwidth** and **Cleansing Traffic**.
>
![](https://main.qcloudimg.com/raw/ea0019a1d66fa4de3b69f131199b2f28.png)

## Configuring CC Attack Alarm Threshold
Scenario: CC Protection is enabled for the Single IP instance “bgp-000005w1”. When the CC protection bandwidth exceeds 2,000 QPS, alarm messages will be sent to the specific user group.
>To set the attack alarm threshold, make sure you have enabled CC protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Resource List** in the left sidebar to enter the Anti-DDoS Pro page. Click **Single IP Instance** to find the instance “bgp-000005w1”, and then click **Protection Configuration** in the line of the instance.
![](https://main.qcloudimg.com/raw/eed3a23439f1eac3cbc07f1a35ad2a7e.png)
2. Click **CC Protection** and set the threshold to 2,000 QPS for the CC attack alarm threshold.
![](https://main.qcloudimg.com/raw/ff070ffa4e34220d929cdceb421c3d81.png)
