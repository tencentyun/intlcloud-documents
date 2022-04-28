Anti-DDoS Advanced (Global Enterprise Edition) supports watermark protection for the messages sent by the application end. Within the range of the UDP and TCP message ports configured, the application end and Anti-DDoS share the same watermark algorithm and key. After the configuration is completed, every message sent from the client will be embedded with the watermark while attack messages will not, so that the attack messages can be identified and discarded. Watermark protection can effectively and comprehensively defend against layer-4 CC attacks, such as analog business packet attacks and replay attacks.

## Prerequisite
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition) instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.
>?This feature is a paid service. Please [contact us](https://intl.cloud.tencent.com/contact-us) for activation.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** > **Configurations** > **DDoS Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the **Watermark Protection** section.
4. Click **Create**. On the pop-up page, enter the required fields and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/4423cab4c25ca96695f2072d3eefe139.png)
5. After the rule is created, it is added to the list. You can click **Key Configuration** to view and configure a key.
![](https://qcloudimg.tencent-cloud.cn/raw/2e595085a08a622e9340e66e603405ce.png)
6. In the pop-up window, you can view or copy the key.
![](https://main.qcloudimg.com/raw/248b74becc853b238793c466a5635cce.png)
7. You can also add or delete a key. A key can be deleted if you have another key. Up to two watermark keys can be created.
![](https://main.qcloudimg.com/raw/2bf90364cfc8bf00ee43646a8e0d30e0.png)
