Anti-DDoS Pro can automatically trigger blocking policies facing abnormal connections. With **Maximum Source IP Exceptional Connections** enabled, a source IP that frequently sends a large number of messages about abnormal connection status will be detected and added to the blocklist. The source IP will be accessible after being blocked for 15 minutes.
>?The following fields are supported:
>- **Source New Connection Rate Limit**: limits the rate of new connections from source ports.
>- **Source Concurrent Connection Limit**: limits the number of active TCP connections from source addresses at any one time.
>- **Destination New Connection Rate Limit**: limits the rate of new connections from destination IP addresses and destination ports.
>- **Destination Concurrent Connection Limit**: limits the number of active TCP connections from destination IP addresses at any one time.
>- **Maximum Source IP Exceptional Connections**: limits the maximum number of abnormal connections from source IP addresses.

## Prerequisites
You have successfully purchased an [Anti-DDoS Pro](https://intl.cloud.tencent.com/document/product/1029/36115) instance and set the protected target.

## Directions
1. Log in to the [Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Configurations** on the left sidebar.
2. Select an Anti-DDoS Pro instance ID in the list on the left, such as "bgp-00xxxxxx".
![](https://main.qcloudimg.com/raw/f3910ce6e7bd09a90bd2526c137a7e62.png)
3. Click **Set** in the **Connection Attack Protection** section to get to configuration.
![](https://main.qcloudimg.com/raw/c511a2a2578e318dc1224e6f7bec5a05.png)
4. Click **Create** to create a connection attack protection rule.
5. In the pop-up window, enable **Connection Flood Protection** and **Abnormal Connection Protection**, and click **OK**.
![](https://main.qcloudimg.com/raw/1cd6b0ba5863c2b90b458a5410a68ea2.png)
6. Now the new rule is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/9dfcd1c64ffd984f65dfac5572077d7e.png)
