
Anti-DDoS supports watermark protection for the messages sent by the application end. Within the range of the UDP and TCP message ports configured, the application end and Anti-DDoS share the same watermark algorithm and key. After the configuration is completed, every message sent from the client will be embedded with the watermark while attack messages will not, so that the attack messages can be identified and discarded. Watermark protection can effectively and comprehensively defend against layer-4 CC attacks, such as analog business packet attacks and replay attacks.

## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select the ID or port of a protected IP from the left list, e.g., **212.64.xx.xx bgpip-000002jt** or **119.28.xx.xx bgpip-000002ju** -> **tcp:8000**. Click **Set** in the **Watermark Protection** section to enter the watermark protection list.
![](https://main.qcloudimg.com/raw/1307aa200b2c60d2c41bf6b96c8ac9dc.png)
3. Click **Create**.
4. In the pop-up window, fill in the configuration fields and click **OK**.
![](https://main.qcloudimg.com/raw/34139b0bc9f783c936641bd95ab199c2.png)
5. Now the new watermark protection rule is added to the list, and you can click **Key Configuration** to view and configure a key.
6. You can view and copy the key.
![](https://main.qcloudimg.com/raw/248b74becc853b238793c466a5635cce.png)
7. You can also add or delete a key on the key configuration page. A key can be deleted if you have another key. Up to two watermark keys can be created.
![](https://main.qcloudimg.com/raw/2bf90364cfc8bf00ee43646a8e0d30e0.png)
