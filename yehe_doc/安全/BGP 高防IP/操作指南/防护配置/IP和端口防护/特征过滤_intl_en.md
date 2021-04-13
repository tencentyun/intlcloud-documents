
Anti-DDoS supports configuring custom blocking policies against specific IP, TCP, UDP message header or payload. After enabling feature filtering, you can combine the matching conditions of the source port, destination port, message length, IP message header or payload, and set the protection action to continue protection, allow/block/discard matched requests, block the IP for 15 minutes, or discard the request and then block the IP for 15 minutes, etc. With feature filtering, you can configure accurate protection policies against business message features or attack message features.

## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select the ID or port of a protected IP from the left list, e.g., **212.64.xx.xx bgpip-000002jt** or **119.28.xx.xx bgpip-000002ju** -> **tcp:8000**. Click **Set** in the **Feature Filtering** section to enter the feature filtering list.
![](https://main.qcloudimg.com/raw/56516d0de6b77e5df9aa5592465f5c4d.png)
3. Click **Create**, fill in the configuration fields, and click **OK**.
![](https://main.qcloudimg.com/raw/775ad163e64f17450dae4ae697011e54.png)
4. Now the new feature filtering rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/11435bbcd6ea6c2b6a762d2a0bd863f3.png)

