Anti-DDoS can automatically trigger blocking policies facing abnormal connections. With **Maximum Source IP Exceptional Connections** enabled, a source IP that frequently sends a large number of messages about abnormal connection status will be detected and added to the blocklist. The source IP will be accessible after being blocked for 15 minutes. You can set the following configurations as needed:
>?
>- **Source New Connection Rate Limit**: limits the rate of new connections from source ports.
>- **Source Concurrent Connection Limit**: limits the number of active TCP connections from source addresses at any one time.
>- **Destination New Connection Rate Limit**: limits the rate of new connections from destination IP addresses and destination ports.
>- **Destination Concurrent Connection Limit**: limits the number of active TCP connections from destination IP addresses at any one time.
>- **Maximum Source IP Exceptional Connections**: limits the maximum number of abnormal connections from source IP addresses.

## Prerequisites
You have purchased an Anti-DDoS Advanced (Global Enterprise Edition) instance and set your target to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) Console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** -> **Configurations** on the left sidebar.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/d6586694f3fc6b1cbc6099b6b1498c38.png)
3. Click **Set** in the **Connection Attack Protection** section to get to configuration.
![](https://main.qcloudimg.com/raw/8e53b26f6ba40eb78c1b2a333a536277.png)
4. Click **Create**.
5. In the pop-up window, enable the protection and click **OK**.
![](https://main.qcloudimg.com/raw/1f3e64929a897e6b605f4c56482ed2a3.png)
6. Now the new connection attack protection rule is added to the list, and you can click **Configuration** to modify it.
![](https://main.qcloudimg.com/raw/54fc09923ef20ab68e5ef84c62a4e4e8.png)
