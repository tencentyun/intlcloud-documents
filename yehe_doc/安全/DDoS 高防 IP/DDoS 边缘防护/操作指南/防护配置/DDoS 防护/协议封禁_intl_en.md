 DDoS Edge Defender supports blocking inbound traffic by blocking protocols such as ICMP, TCP and UDP. When you complete the configuration, the access requests will be blocked directly. Of these protocols, UDP as a connectionless protocol dose not provide a three-way handshake process like TCP, and thus has security vulnerabilities. We recommend blocking UDP if it is not used for your application.

## Prerequisites
You have successfully purchased a [DDoS Edge Defender](https://intl.cloud.tencent.com/document/product/297/42172) instance and set the object to protect.

>? DDoS Edge Defender is currently available to beta users. To use it, please [contact us](https://intl.cloud.tencent.com/contact-us).

## Directions
1. Log in to the [DDoS Edge Defender Console](https://console.cloud.tencent.com/ddos/antiddos-edge/policy/ddos), click **Protection Policy** on the left sidebar, and then select the tab **DDoS Protection**.
2. Select an Edge Defender instance ID, such as "edge-xxxxxxx".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the **Block by Protocol** section on the right.
![](https://main.qcloudimg.com/raw/e5c2d1901cf5b9c793b770a91e79814a.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields and click **OK**.
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
6. Now the new is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)
