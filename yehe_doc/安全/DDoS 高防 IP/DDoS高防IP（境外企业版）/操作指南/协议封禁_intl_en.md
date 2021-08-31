Anti-DDoS supports blocking the source traffic accessing Anti-DDoS instances based on specified protocols, such as ICMP, TCP, UDP, and other protocols. After the configuration is completed, all matched access requests will be directly blocked. Due to the connectionless feature of UDP protocol (unlike TCP, which requires a three-way handshake process), it has natural security vulnerabilities. If you do not have UDP businesses, we recommend blocking the UDP protocol.

## Prerequisites
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition)](https://cloud.tencent.com/document/product/1014/56255) instance and set your target to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/d6586694f3fc6b1cbc6099b6b1498c38.png)
3. Click **Set** in the **Block by Protocol** block on the right.
![](https://main.qcloudimg.com/raw/470184647b0853c1bbc8dc2654bfc027.png)
4. Click **Create**.
5. In the pop-up window, fill in the configuration fields and click **OK**.
![](https://main.qcloudimg.com/raw/282c775d40be4ad528f3ce66177a5537.png)
6. Now the new protocol blocking rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/aac0f7e37844d0a1b9fa6407ae5a9775.png)
