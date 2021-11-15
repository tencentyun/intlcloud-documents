 DDoS Edge Defender supports configuring custom blocking policies against specific IP, TCP, UDP message header and payload. After enabling feature filtering, you can combine the matching conditions of the source port, destination port, message length, IP message header and payload, and set the protection action to continue protection, allow/block/discard matched requests, block the IP for 15 minutes, or discard the request and then block the IP for 15 minutes, etc. With feature filtering, you can configure accurate protection policies against business message features or attack message features.


## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.

>? DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select the tab **DDoS Protection**.
2. Select an Edge Defender instance ID, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the **Feature Filtering** section on the right.
![](https://main.qcloudimg.com/raw/56516d0de6b77e5df9aa5592465f5c4d.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields, and click **OK**.
![](https://main.qcloudimg.com/raw/775ad163e64f17450dae4ae697011e54.png)
6. Now the new rule is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/11435bbcd6ea6c2b6a762d2a0bd863f3.png)
