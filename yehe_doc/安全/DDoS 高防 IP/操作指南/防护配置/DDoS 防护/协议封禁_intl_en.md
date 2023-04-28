Anti-DDoS supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
- You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the target to protect.

## Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/config/port) and select **Anti-DDoS Advanced (New)** > **Configurations** on the left sidebar. Open the **DDoS Protection** tab.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "bgpip-xxxxxx".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the "Protocol blocking" section.
![](https://qcloudimg.tencent-cloud.cn/raw/265fb9c70725dff7d10744603f876972.png)
4. Click **Create**.
>?The **Create** button appears only when you use this feature for the first time.

5. In the pop-up window, click the button on the right of a protocol, and click **Confirm**.
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
6. After the rule is created, it is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)

