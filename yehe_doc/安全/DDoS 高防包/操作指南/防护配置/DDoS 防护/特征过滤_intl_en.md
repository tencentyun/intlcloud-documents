Anti-DDoS Pro supports configuring custom blocking policies against specific IP, TCP, UDP message header or load. After enabling feature filtering, you can combine the matching conditions of the source port, destination port, message length, IP message header or load, and set the protection action to allow/block/discard matched requests, block the IP for 15 minutes, discard the request and block the IP for 15 minutes, or continue protection, etc. With feature filtering, you can configure precise protection policies against business message features or attack message features.

## Prerequisites

You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the new [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and select **Anti-DDoS Pro (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/9cf812dc64f1dcd113fc2f35534544b5.png)
3. Click **Set** in the **Port Filtering** section to enter the port filtering page.
![](https://qcloudimg.tencent-cloud.cn/raw/8560684be1e643ce0eb00a3dad1e0f50.png)
4. Click **Create** to create a feature filtering rule.
5. In the pop-up window, fill in the configuration fields, and click **OK**.
![](https://main.qcloudimg.com/raw/8cc71c584f2514fd432c9579a716c96b.png)
6. After the rule is created, it is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/dbf8f257ae3cdeb0d30a96a2e7ef4d1d.png)
