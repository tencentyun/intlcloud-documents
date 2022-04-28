Anti-DDoS Advanced (Global Enterprise Edition) can automatically trigger blocking policies facing abnormal connections. With **Maximum Source IP Exceptional Connections** enabled, a source IP that frequently sends a large number of messages about abnormal connection status will be detected and added to the blocklist. The source IP will be accessible after being blocked for 15 minutes. You can set the following configurations as needed:
>?
>- **Source New Connection Rate Limit**: limits the rate of new connections from source ports.
>- **Source Concurrent Connection Limit**: limits the number of active TCP connections from source addresses at any one time.
>- **Destination New Connection Rate Limit**: limits the rate of new connections from destination IP addresses and destination ports.
>- **Destination Concurrent Connection Limit**: limits the number of active TCP connections from destination IP addresses at any one time.
>- **Maximum Source IP Exceptional Connections**: limits the maximum number of abnormal connections from source IP addresses.

## Prerequisite
You have purchased an [Anti-DDoS Advanced (Global Enterprise Edition)](https://intl.cloud.tencent.com/document/product/297/41154) instance and set the object to protect.

## Directions
1. Log in to the [Anti-DDoS Advanced (Global Enterprise Edition) console](https://console.cloud.tencent.com/ddos/ddos-basic) and select **Anti-DDoS Advanced** > **Configurations** > **DDoS Protection**.
2. Select an Anti-DDoS Advanced instance ID in the list on the left, such as "xxx.xx.xx.xx bgpip-000003n2".
![](https://main.qcloudimg.com/raw/9c8bb19be4726a46a2261b35e048c8cb.png)
3. Click **Set** in the **Connection Attack Protection** section.
4. Click **Create**. On the pop-up page, configure the protection settings and click **OK**.
![](https://main.qcloudimg.com/raw/8e8a016568eb8f10efc8351c70fdb05f.png)
6. After the rule is created, it is added to the list. You can click **Configuration** on the right of the rule to modify it.
![](https://main.qcloudimg.com/raw/88b4468cd4c49af24705c16551fb42e3.png)
