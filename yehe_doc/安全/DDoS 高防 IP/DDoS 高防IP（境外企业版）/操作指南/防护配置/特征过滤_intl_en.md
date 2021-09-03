Anti-DDoS supports configuring custom blocking policies against specific IP, TCP, UDP message header or payload. After enabling feature filtering, you can combine the matching conditions of the source port, destination port, message length, IP message header or payload, and set the protection action to continue protection, allow/block/discard matched requests, block the IP for 15 minutes, or discard the request and then block the IP for 15 minutes, etc. With feature filtering, you can configure accurate protection policies against business message features or attack message features.

## Prerequisites
You have purchased an Anti-DDoS Advanced (Global Enterprise Edition) instance and set your target to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/d6586694f3fc6b1cbc6099b6b1498c38.png)
3. Click **Set** in the **Feature Filtering** section to enter the feature filtering page.
![](https://main.qcloudimg.com/raw/6329c781ac16d4599d17c28e0f0d2d56.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields, and click **OK**.
![](https://main.qcloudimg.com/raw/660254c7e73ecfddd962614a2439bf81.png)
6. Now the new feature filtering rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/0f65892f5e1fbb4f626ce54bbf9dbd60.png)
