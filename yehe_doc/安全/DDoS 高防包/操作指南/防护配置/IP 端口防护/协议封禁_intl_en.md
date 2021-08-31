
Anti-DDoS Pro supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the [Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Configurations** on the left sidebar.
Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/ceb4f1ebedc2efb78e428f5ffe071473.png)
3. Click **Set** in the **Block by Protocol** section on the right.
![](https://main.qcloudimg.com/raw/fa38ed5eb9bb5bcf4d1668f9b4c6d807.png)
4. Click **Create** to create a protocol blocking rule.
![](https://main.qcloudimg.com/raw/10d37670faa7de3167d8cdeb4cf85e61.png)
5. In the pop-up window, click to enable the protocol, and click **OK**.
![](https://main.qcloudimg.com/raw/58a617dbd1909430bf41de75fe34ed39.png)
6. Now the new is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/da1c3776c49b90c1d6f8b7dca0f2c41a.png)
