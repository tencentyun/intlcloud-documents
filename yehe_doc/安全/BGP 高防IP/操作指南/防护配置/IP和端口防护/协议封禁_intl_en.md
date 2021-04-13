
Anti-DDoS supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select the ID or port of a protected IP from the left list, e.g., **212.64.xx.xx bgpip-000002jt** or **119.28.xx.xx bgpip-000002ju** -> **tcp:8000**. Click **Set** in the **Block by protocol** section to enter the list.
![](https://main.qcloudimg.com/raw/d98fce7a7f7664f1153a921e8417d01f.png)
3. Click **Create**.
4. In the pop-up window, fill in the configuration fields and click **OK**.
![](https://main.qcloudimg.com/raw/2b862288e7aa29b0470e4be5b2e94be4.png)
5. Now the new protocol blocking rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/6eb66d6d739b3ea4eea0e23e0588c3a1.png)

