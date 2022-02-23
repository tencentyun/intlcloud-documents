Anti-DDoS Pro supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and select **Anti-DDoS Pro (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
  ![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)

  
3. Click **Set** in the **Block by Location** section.
![](https://qcloudimg.tencent-cloud.cn/raw/3f04c6afa6e8d7f93caaf184edca77ad.png)
4. Click **Create** to create a protocol blocking rule.
![](https://main.qcloudimg.com/raw/10d37670faa7de3167d8cdeb4cf85e61.png)
5. In the pop-up window, click the button on the right of a protocol, and click **Confirm**.
![](https://main.qcloudimg.com/raw/58a617dbd1909430bf41de75fe34ed39.png)
6. After the rule is created, it is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/da1c3776c49b90c1d6f8b7dca0f2c41a.png)
