Anti-DDoS supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
You have purchased an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the **Block by Protocol** section on the right.
![](https://main.qcloudimg.com/raw/e5c2d1901cf5b9c793b770a91e79814a.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields and click **OK**.
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
6. Now the new is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)


