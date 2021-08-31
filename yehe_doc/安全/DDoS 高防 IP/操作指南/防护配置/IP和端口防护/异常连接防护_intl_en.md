
When a source IP initiates a number of abnormal connections that exceed the threshold, Anti-DDoS can automatically block the IP. After the abnormal connection protection is enabled, if a source IP sends a large volume of messages with abnormal connection status frequently in a short period, the source IP will be blocked for 15 minutes and recovered automatically after that.

## Prerequisites
Purchase an [Anti-DDoS Advanced instance](https://intl.cloud.tencent.com/document/product/297/37241) and set the object to be protected.

## Operation Directions
1. Log in to the [Anti-DDoS console](https://console.cloud.tencent.com/ddos/antiddos-advanced/package) and click **Anti-DDoS Advanced (New)** -> **Configurations** on the left sidebar.
2. Select the ID or port of a protected IP from the left list, e.g., **212.64.xx.xx bgpip-000002jt** or **119.28.xx.xx bgpip-000002ju** -> **tcp:8000**. Click **Set** in the **Abnormal Connection Protection** section to enter the abnormal connection protection list.
![](https://main.qcloudimg.com/raw/f7e8a12e1d056a4ef00ca0741685974f.png)
3. Click **Create**.
4. In the pop-up window, enable the protection and click **OK**.
![](https://main.qcloudimg.com/raw/5998491511d937b5d3e5c12635d331a0.png)
5. Now the new abnormal connection protection rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/4774d8db4b83a4c913f5db560243ce5b.png)
