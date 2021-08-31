The non-website business protection service of Anti-DDoS Advanced provides IP-based session persistence to support forwarding requests from the same IP address to the same real server for processing.
Layer-4 forwarding supports simple session persistence. The session persistence duration can be set to any integer between 30 and 3,600 seconds. If the time threshold is exceeded and the session has no new request, the connection will be automatically closed.


## Directions
1. Log in to the [new Anti-DDoS Advanced Console](https://console.cloud.tencent.com/ddos/antiddos-advanced/access/l4) and click **Business Connection** on the left sidebar. On the business connection page, click **Port Connection** to enter the corresponding management page.
2. On the "Port Connection" tab, select the target Anti-DDoS Advanced instance and the corresponding rule and click **Edit** in the "Session Persistence" column.
![](https://main.qcloudimg.com/raw/dd5886459c00c1c9f50dc0af103b7bba.png)
3. On the session persistence editing page, set the persistence duration and click **OK**.
>? Session persistence is disabled by default. When setting the persistence duration, you are recommended to use the default value.
>
![](https://main.qcloudimg.com/raw/ab55b52a20af19f140cea4167a168371.png)


