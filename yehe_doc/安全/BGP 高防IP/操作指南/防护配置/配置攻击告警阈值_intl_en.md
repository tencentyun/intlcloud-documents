## Use Cases
When attacks against your Anti-DDoS Advanced resources start/end and your protected IPs are blocked/unblocked, you will get notifications through internal message, SMS, or email. Configuring proper attack alarm thresholds can help you know more about attacks instantly. This feature can also help prevent false alarming caused by normal business operations that bring traffic surges (such as data sync). For more information on how to receive alarm messages, please see [Setting Security Event Notification](https://intl.cloud.tencent.com/document/product/297/15553).
## Configuring DDoS Attack Alarm Threshold
This configuration example can achieve the following effect: after the attack traffic to the Anti-DDoS Advanced instance "bgpip-0000021y" exceeds the cleansing threshold and triggers DDoS attack cleansing, when the cumulative cleansed traffic (value) exceeds 1,000 Mbps, DDoS attack alarm messages will be sent to the specified user group.
>To set the attack alarm threshold, make sure that you have enabled DDoS protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2), select **Anti-DDoS Advanced** > **Resource List** on the left sidebar to enter the Anti-DDoS Advanced page, find the instance "bgpip-0000021y", and click **Protection Configuration** in the "Operation" column.

2. Enter the DDoS protection configuration page, select the alarm metric **Cleansed Traffic** in the drop-down list on the right of the DDoS attack alarm threshold, and set the threshold to 1,000 Mbps.
>The DDoS attack alarm threshold is **Not Set** by default. Available alarm metrics include **Inbound Traffic Bandwidth** and **Cleansed Traffic**.
>

## Configuring CC Attack Alarm Threshold
This configuration example can achieve the following effect: after the Anti-DDoS Advanced instance "bgpip-0000021y" triggers CC protection, when the HTTP CC protection bandwidth exceeds 2000 QPS, CC attack alarm messages will be sent to the specified user group.
>To set the attack alarm threshold, make sure that you have enabled HTTP CC protection.

1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Anti-DDoS Advanced** > **Protection Configuration**. On the protection configuration page, click **CC Protection**.
2. On the CC protection page, find the "HTTP CC Protection" section at the bottom of the page, and set the threshold to 2,000 QPS in "HTTP CC Attack Alarm Threshold".
